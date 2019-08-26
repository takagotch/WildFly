### wildfly
---
https://github.com/wildfly/wildfly

http://www.wildfly.org/

```java
public class TransactionsBootstrapDependencyInstaller implements BootstrapDependencyInstaller {
  
  @Override
  public ServiceName install(ServiceTarget serviceTarget, DeploymentUnit deploymentUnit, boolean jtsEnabled) {
    final ServiceName weldTransactionServiceName = deploymentUnit.getServiceName().append(WeldTransactionServices.SERVICE_NAME);
    final ServiceBuilder<?> sb = serviceTarget.addService(weldTransactionServiceName);
    final Consumer<WeldTransactionServices> weldTransactionServicesConsumer = sb.providers(weldTransactionServiceName);
    sb.requires(ServiceNames.capabilityServiceName(deploymentUnit, "org.wildflytransactions.global-default-local-provider"));
    sb.setInstance(new WeldTransactionServices(jtsEnabled, weldTransactionServicesConsumer));
    sb.install();
    
    return weldTransactionServiceName;
  }
}
```

```sh
mvn install 
./mvnw install
mvnw install
./domain.sh
./standalone.sh
./jboss-cli.sh --connect command=:shutdown
mvn install -DallTests
```

```
```


