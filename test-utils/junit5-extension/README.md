# camunda-bpm-junit5

Extension that allows you to write process tests using JUnit5.

## Usage

### Maven dependency
Add the dependency to your pom.xml

    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-bpm-junit5</artifactId>
      <version>7.17.0</version>
      <scope>test</scope>
    </dependency>

### Test code
Add the annotation to your test class:

    @ExtendWith(ProcessEngineExtension.class)
    
For further access provide a field where the process engine gets injected:

    public ProcessEngine processEngine; 
    
Or register the extension from the builder:

    @RegisterExtension
    ProcessEngineExtension extension = ProcessEngineExtension.builder()
      .configurationResource("audithistory.camunda.cfg.xml")
      .build();
    
and access the process engine from the extension object:

    RuntimeService runtimeService = extension.getProcessEngine().getRuntimeService(); 

If you don't want to create a configuration file, you can add a process engine, that you configure programmatically:

    public ProcessEngine myProcessEngine = ProcessEngineConfiguration
        .createStandaloneInMemProcessEngineConfiguration()
        .setJdbcUrl("jdbc:h2:mem:camunda;DB_CLOSE_DELAY=1000")
        .buildProcessEngine();
    
    @RegisterExtension
    ProcessEngineExtension extension = ProcessEngineExtension
        .builder()
        .useProcessEngine(myProcessEngine)
        .build();

    
