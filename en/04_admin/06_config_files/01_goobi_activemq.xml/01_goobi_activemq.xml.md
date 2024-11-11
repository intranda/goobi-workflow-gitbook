# goobi_activemq.xml

The `goobi_activemq.xml` configuration file specifies the settings for the `org.apache.activemq` Java library used by Goobi Workflow.

Goobi Workflow does not use the file itself, but passes it directly to the library as configuration. This documentation only presents the most important settings that are relevant for Goobi. More detailed documentation can be found on the activemq website.

The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_activemq.xml
```

For example, this configuration file looks as follows:

{% code title="goobi_activemq.xml" %}
```xml
<beans
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:amq="http://activemq.apache.org/schema/core"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://activemq.apache.org/schema/core http://activemq.apache.org/schema/core/activemq-core.xsd">
    <broker xmlns="http://activemq.apache.org/schema/core" brokerName="localhost" schedulerSupport="true" schedulerDirectory="/opt/digiverso/goobi/activemq/scheduler">
        <transportConnectors>
            <transportConnector name="stomp" uri="stomp://localhost:61613" />
            <transportConnector name="tcp" uri="tcp://localhost:61616" />
        </transportConnectors>
        <persistenceAdapter>
            <kahaDB directory="/opt/digiverso/goobi/activemq/messages" journalMaxFileLength="32mb" />
        </persistenceAdapter>
        <systemUsage>
            <systemUsage>
                <memoryUsage>
                    <memoryUsage limit="64 mb"/>
                </memoryUsage>
                <storeUsage>
                    <storeUsage limit="512 mb"/>
                </storeUsage>
                <tempUsage>
                    <tempUsage limit="128 mb"/>
                </tempUsage>
            </systemUsage>
        </systemUsage>
        <managementContext>
            <managementContext createConnector="false"/>
        </managementContext>
        <plugins>
            <redeliveryPlugin fallbackToDeadLetter="true"
                sendToDlqIfMaxRetriesExceeded="true">
                <redeliveryPolicyMap>
                    <redeliveryPolicyMap>
                        <redeliveryPolicyEntries>
                            <redeliveryPolicy queue="goobi_fast"
                                maximumRedeliveries="5"
                                initialRedeliveryDelay="10000"
                                backOffMultiplier="1.5"
                                useExponentialBackOff="true"/>
                        </redeliveryPolicyEntries>
                        <defaultEntry>
                            <!-- the fallback policy for all other destinations -->
                            <redeliveryPolicy maximumRedeliveries="10"
                                initialRedeliveryDelay="300000"
                                backOffMultiplier="1.5"
                                useExponentialBackOff="true"/>
                        </defaultEntry>
                    </redeliveryPolicyMap>
                </redeliveryPolicyMap>
            </redeliveryPlugin>
            <simpleAuthenticationPlugin>
                <users>
                    <authenticationUser username="goobi" password="goobi"
                        groups="admins,publishers,consumers"/>
                    <authenticationUser username="worker" password="worker"
                        groups="consumers"/>
                </users>
            </simpleAuthenticationPlugin>
            <authorizationPlugin>
                <map>
                    <authorizationMap>
                        <authorizationEntries>
                            <authorizationEntry topic=">" read="admins" write="admins" admin="admins" />
                            <authorizationEntry queue=">" read="admins" write="admins" admin="admins" />
                            <authorizationEntry queue="goobi_fast" read="consumers" write="publishers" admin="publishers" />
                            <authorizationEntry queue="goobi_slow" read="consumers" write="publishers" admin="publishers" />
                            <authorizationEntry queue="goobi_status" read="admins" write="consumers" />
                        </authorizationEntries>
                    </authorizationMap>
                </map>
            </authorizationPlugin>
        </plugins>
    </broker>
</beans>
```
{% endcode %}

## XML namespaces used

This configuration file can use multiple XML namespaces in more complex applications.

The root element `<beans>` always uses this default namespace:

```xml
xmlns="http://www.springframework.org/schema/beans"
```

The `<broker>` sub-element always uses this default namespace:

```xml
xmlns="http://activemq.apache.org/schema/core"
```

## Settings for the Message Broker

All settings that are important for using the Message Broker of Goobi Workflow are made inside the `<broker>` element.

The `brokerName` parameter is used to specify the name of the message broker. Since this is the only one on localhost (on this computer system), the name defaults to `localhost`.

The `schedulerSupport` parameter specifies whether a scheduler is used for multithreading.

The `schedulerDirectory` parameter specifies a full file path to an executable scheduler.

### Enabling URIs with specific protocol

The `<transportConnectors>` element is used to specify a list of enabled endpoints along with the protocols that can be used. Each `<transportConnector>` element contained in it specifies an endpoint.

An endpoint usually has two parameters. The `name` parameter specifies a name for the enablement. For example, this can be the name of the protocol. The `uri` parameter specifies a Uniform Resource Identifier consisting of a protocol, an IP address or domain, a port number, a path and any parameters. From the URL specified here, activemq can later be accessed using the specified port and protocol.

### Database used

It can happen that transmitted information is not directly accepted by the receiver. If this information is not requested for a long enough time, activemq stores it in its own database. This is configured with the `<persistenceAdapter>` element.

By default `kahaDB` is used, so the configuration includes an element `<kahaDB>` with the parameter `directory`, specifying the full file path to the database.

Additionally, the `journalMaxFileLength` parameter can be specified to limit the file size in the database. One of the units `mb` or `gb` will be used.

### Memory limit

The `<systemUsage>` element can be used to limit the available memory for the transferred data in the queue.

The `<memoryUsage>` element defines the maximum size of used memory.

The `<storeUsage>` element defines the maximum size of the internal database.

The `<tempUsage>` element defines the maximum size of temporary files.

The most common units for the `limit` parameter are `mb` and `gb`.

### Custom connection for JMX

The `<managementContext>` element is usually used to turn off a custom connection for JMX (Java Management Extensions). The `createConnector` parameter is set to `false` by default to use the default connection.

### Plugins

This configuration of the Message Broker by default comes with three plugins that handle authentication and the redelivery system.

#### Plugin for user groups

The `<authenticationPlugin>` is used to define user groups and their access rights to different queues.

With each `<authorizationEntry>` a queue and its details are specified. The `queue` parameter specifies the used queue. The `topic` parameter can be used to configure access to specific topics instead of read and write permissions for a queue.

Instead of a name, the value `>` can be set for a queue or topic. This is a universal operator and applies to all queues and topics.

The `read`, `write` and `admin` parameters specify user groups that have read, write and administrator access to the respective queue or topic respectively. Multiple user groups in one parameter can be separated with comma.

#### Plugin for users and passwords

The `<simpleAuthenticationPlugin>` is used to create users and define passwords and user groups for users. Each `<authenticationUser>` element specifies an authenticatable user. The `username` and `password` parameters define the username and the necessary password with which the user (or other software) must authenticate.

In addition, there is the `groups` parameter, which contains a comma-separated list of user groups to which the respective user belongs. These groups are relevant for the `<authorizationPlugin>`.

#### Plugin for error handling

The `<redeliveryPlugin>` is used to configure more detailed error handling for resending data that was transmitted with errors. This plugin has two boolean parameters that control the final save of multiple failed transmission attempts and their contents.

With the `fallbackToDeadLetter` parameter, messages are not retransmitted after a certain number of failed transmission attempts to keep the system load low.

With the parameter `sendToDlqIfMaxRetriesExceeded` a message that could not be sent several times is written to a residual memory. There it remains until it can be read manually or by a later successful transmission attempt. This prevents the queuing system from being overloaded with non-functional connections.

The sub-element `<redeliveryPolicyEntries>` lists error handling rules that should apply to specific queues. For each rule entered there, the element `<redeliveryPolicy>` and the parameter `queue` define the corresponding queue.

In the element `<defaultEntry>` the default case is defined, which will be executed if none of the above rules apply. This element `<redeliveryPolicy>` defines exactly one rule, but this one does not need a `queue` parameter, because it is used for all queues in all usual cases.

Some more parameters can be specified for the rules. For example, with the integer `maximumRedeliveries` parameter it is possible to specify the maximum number of attempts before a message is written to the residual memory. The `initialRedeliveryDelay` parameter, also an integer, is used to specify the number of milliseconds after which a new transmission attempt is started.

To avoid a permanent load on the system, the time interval between retransmission attempts can be increased exponentially each time. For this the boolean parameter `useExponentialBackOff` is set to `true` and with the parameter `backOffMultiplier` a multiplication factor is specified, with which the period is increased. For example, if this is set to 1.5 and the initial period is set to 60 seconds, the next send attempt will be executed after 1.5 * 60 = 90 seconds. The third follows after another 1.5 * 90 = 135 seconds.