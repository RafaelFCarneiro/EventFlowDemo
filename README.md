EventFlowDemo

A working example of how to setup eventflow for a web api application using .net core 2.2. I will be making improvements as i learn more about EventFlow.

## Endpoints 

There are 2 endpoint available, one to create new example requests which in turn emit new events and one to retrieve the read data model

[POST] /api/examples 

[GET]  /api/examples/example-f134268c-de10-4740-817b-a2627aa3f8b7


## Configuration 

This basic template uses Autofaq as provided by EventFlow, and uses the file store for the persisting of the events. The event store is created at the root of the application. The read store is configured to use in-memory so if the application restarts, the read states will be lost.

```
var container = EventFlowOptions.New
                .UseAutofacContainerBuilder(containerBuilder)
                .AddAspNetCoreMetadataProviders()
                .AddEvents(typeof(ExampleEvent))
                .AddCommands(typeof(ExampleCommand))
                .AddCommandHandlers(typeof(ExampleCommandHandler))
                .UseConsoleLog()
                .UseFilesEventStore(FilesEventStoreConfiguration.Create("./evt-store"))
                .UseInMemoryReadStoreFor<ExampleReadModel>();
```
