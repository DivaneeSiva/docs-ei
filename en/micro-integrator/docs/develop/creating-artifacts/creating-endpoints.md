# Creating an Endpoint
Follow the instructions given below to create a new REST API artifact in WSO2 Integration Studio.

## Instructions

1.  If you have already created an [ESB Config project](../../creating-projects/#esb-config-project), right-click the project and go to **New → Endpoint** to open the **New Endpoint Artifact** dialog.
2.  Select **Create a New Endpoint** and click **Next**.
3.  Type a unique name for the endpoint, and then specify the type of
    endpoint you are creating.

    <table>
        <tr>
            <th>Endpoint Type</th>
            <th>Description</th>
        </tr>
        <tr>
            <td><b>Address Endpoint</b></td>
            <td>Defines the direct URL of the service.</td>
        </tr>
        <tr>
            <td><b>Default Endpoint</b></td>
            <td>Defines additional configuration for the default target.</td>
        </tr>
        <tr>
            <td><b>Failover Endpoints</b></td>
            <td>Defines the endpoints that the service will try to connect to in case of a failure. This will take place in a round robin manner.</td>
        </tr>
        <tr>
            <td><b>HTTP Endpoint</b></td>
            <td>Defines a URI template based REST service endpoint.</td>
        </tr>
        <tr>
            <td><b>Load Balance Endpoint</b></td>
            <td>Defines groups of endpoints for replicated services. The incoming requests will be directed to these endpoints in a round robin manner. These endpoints automatically handle the fail-over cases as well.</td>
        </tr>
        <tr>
            <td><b>Recipient List Group</b></td>
            <td>Defines the list of endpoints a message will be routed to.</td>
        </tr>
        <tr>
            <td><b>Template Endpoint</b></td>
            <td>Allows to create a custom Endpoint template.</td>
        </tr>
        <tr>
            <td><b>WSDL Endpoint</b></td>
            <td>Defines the WSDL, service and port.</td>
        </tr>
    </table>

4.  Do one of the following:  
    -   To save the endpoint in an existing ESB Config project in your workspace, click **Browse** and select that project.
    -   To save the endpoint in a new ESB Config project, click **Create new Project** and create the new project.
    -   To save the endpoint in a Registry Resource Project, click **Make this a Dynamic Endpoint**, click the **Browse** button next to **Save endpoint in** and select the registry, and then select the registry (Configuration or Governance) where you want to save the endpoint. Lastly, type the endpoint name in the **Registry Path** box.

5.  Click **Finish** . The endpoint is created in the `          endpoints         ` folder under the ESB Config or Registry Resource project you specified, and the endpoint opens in the editor.

## Properties

``` java tab='Address Endpoint'
<address uri="endpoint address" [format="soap11|soap12|pox|rest|get"] [optimize="mtom|swa"]
        [encoding="charset encoding"]
        [statistics="enable|disable"] [trace="enable|disable"]>
    
    <enableSec [policy="key"]/>?
    <enableAddressing [version="final|submission"] [separateListener="true|false"]/>?
    
    <timeout>
        <duration>timeout duration in milliseconds</duration>
        <responseAction>discard|fault</responseAction>
    </timeout>?
    
    <markForSuspension>
        [<errorCodes>xxx,yyy</errorCodes>]
        <retriesBeforeSuspension>m</retriesBeforeSuspension>
        <retryDelay>d</retryDelay>
    </markForSuspension>
    
    <suspendOnFailure>
        [<errorCodes>xxx,yyy</errorCodes>]
        <initialDuration>n</initialDuration>
        <progressionFactor>r</progressionFactor>
        <maximumDuration>l</maximumDuration>
    </suspendOnFailure>
</address>
```

``` java tab='Default Endpoint'
<default [format="soap11|soap12|pox|get"] [optimize="mtom|swa"]
         [encoding="charset encoding"]
         [statistics="enable|disable"] [trace="enable|disable"]>
    
    <enableRM [policy="key"]/>?
    <enableSec [policy="key"]/>?
    <enableAddressing [version="final|submission"] [separateListener="true|false"]/>?
    
    <timeout>
        <duration>timeout duration in milliseconds</duration>
        <action>discard|fault</action>
    </timeout>?
    
    <markForSuspension>
        [<errorCodes>xxx,yyy</errorCodes>]
        <retriesBeforeSuspension>m</retriesBeforeSuspension>
        <retryDelay>d</retryDelay>
    </markForSuspension>
    
    <suspendOnFailure>
        [<errorCodes>xxx,yyy</errorCodes>]
        <initialDuration>n</initialDuration>
        <progressionFactor>r</progressionFactor>
        <maximumDuration>l</maximumDuration>
    </suspendOnFailure>
</default>
```

``` java tab='Load Balance Endpoint'
<session type="http|simpleClientSession"/>?
<loadBalance [policy="roundRobin"] [algorithm="impl of org.apache.synapse.endpoints.algorithms.LoadbalanceAlgorithm"]
            [failover="true|false"]>
  <endpoint .../>+
  <member hostName="host" [httpPort="port"] [httpsPort="port2"]>+
</loadBalance>
```

``` java tab='WSDL Endpoint'
<wsdl [uri="wsdl-uri"] service="qname" port/endpoint="qname">
        <wsdl:definition>...</wsdl:definition>?
        <wsdl20:description>...</wsdl20:description>?
        <enableRM [policy="key"]/>?
        <enableSec [policy="key"]/>?
        <enableAddressing/>?
    
    <timeout>
        <duration>timeout duration in milliseconds</duration>
        <action>discard|fault</action>
    </timeout>?
    
    <markForSuspension>
        [<errorCodes>xxx,yyy</errorCodes>]
        <retriesBeforeSuspension>m</retriesBeforeSuspension>
        <retryDelay>d</retryDelay>
    </markForSuspension>
    
    <suspendOnFailure>
        [<errorCodes>xxx,yyy</errorCodes>]
        <initialDuration>n</initialDuration>
        <progressionFactor>r</progressionFactor>
        <maximumDuration>l</maximumDuration>
    </suspendOnFailure>
</wsdl>
```

``` java tab='Dynamic Load Balancing'
<dynamicLoadbalance [policy="roundRobin"] [failover="true|false"]>
    <membershipHandler class="impl of org.apache.synapse.core.LoadBalanceMembershipHandler">
        <property name="name" value="value"/>
    </membershipHandler>
</dynamicLoadbalance>
```

### Basic Properties

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>The name of the endpoint property.</td>
    </tr>
    <tr>
        <td>Format</td>
        <td>
            The message format for the endpoint. The available values are as follows.
            <ul>
                <li>Leave As-Is: If this is selected, no transformation is done to the outgoing message.</li>
                <li>SOAP 1.1: If this is selected the message is transformed to SOAP 1.1.</li>
                <li>SOAP 1.2: If this is selected the message is transformed to SOAP 1.2.</li>
                <li>Plain Old XML (POX): If this is selected the message is transformed to plain old XML format.</li>
                <li>Representational State Transfer (REST): If this is selected, the message is transformed to REST.</li>
                <li>GET: If this is selected, the message is transformed to a HTTP Get Request.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Trace Enabled</td>
        <td> 
            This enables trace for the endpoint. 
        </td>
    </tr>
    <tr>
        <td>Statistics Enabled</td>
        <td>
            This enables statistics for the endpoint.
        </td>
    </tr>
    <tr>
        <td>Build Message</td>
        <td>Only for <b>Failover Endpoint</b> and <b>LoadBalance Endpoint</b></td>
    </tr>
    <tr>
        <td>Algorithm</td>
        <td><b>only for LoadBalance endpoint</b>
            The algorithm on which the load balancing is based. <strong>Round</strong> <strong>Robin</strong> is the default algorithm. You can also load a custom algorithm. Instructions for creating a custom algorithm are included in <a href="http://supunk.blogspot.com/2010/02/writing-load-balance-algorithm-for-wso2.html">this article</a>.
            The `policy` attribute of the load balance element specifies the load balance policy (algorithm) to be used for selecting the target endpoint or static member. <b>Note</b>: Currently only the `roundRobin` policy is supported.
        </td>
    </tr>
    <tr>
        <td>Failover</td>
        <td>
            The `          failover         ` attribute determines if the next endpoint or static member should be selected once the currently selected endpoint or static member has failed, and defaults to true.</br> The <b>failover</b> attribute mentioned above is not applicable for session affinity based endpoints and it is always considered as set to false. If it is required to have failover behavior in session affinity based load balance endpoints, list failover endpoints as the target endpoints.
        </td>
    </tr>
</table>

Failover/LoadBalancing Endpoint properties:

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Endpoint Type</td>
        <td>
            The set of endpoints or static members among which the load has to be distributed. These endpoints can belong to any endpoint type. For example, Failover Endpoints can be listed inside the Load-balance endpoint to load balance between failover groups etc.
        </td>
    </tr>
    <tr>
        <td>Endpoint Value</td>
        <td></td>
    </tr>
</table>

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
      <tr class="even">
         <td>URI</td>
         <td>The address of the endpoint (e.g., <a href="http://wso2.com">http://wso2.com</a> ).</td>
      </tr>
      <tr>
         <td>Target Template</td>
         <td>
            The endpoint template which should be used to define the endpoint. This is specified by selecting one of the existing templates from the <strong>Available Templates</strong> list. The parameters to be included in the endpoint you are defining will be copied from the target template. The values for these parameters can be entered in the <strong>Template Endpoint Parameters</strong> section shown below. Click <strong>Delete Parameter</strong> to remove a parameter fetched from the target template.
         </td>
      </tr>
      <tr>
          <td>Parameters</td>
          <td>
              The parameters of the endpoint. For example, you can add <code>name</code> to add the parameter name, and <code>uri</code> to add the address etc.
          </td>
      </tr>
</table>

### Session Management Properties

For LoadBalance endpoint.

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Session Management</td>
        <td>
            The optional session element makes the endpoint a session affinity based load balancing endpoint. If it is specified, sessions are bound to endpoints in the first message and all successive messages for those sessions are directed to their associated endpoints.
            A session management method from the load balancing group. The possible values are as follows.
            <ul>
               <li>None: If this is selected, session management is not used.</li>
               <li>Transport: If this is selected, session management is done on the transport level using HTTP cookies.</li>
               <li>SOAP: If this is selected, session management is done using SOAP sessions.</li>
               <li>Client ID: If this is selected, session management is done using an ID sent by the client.</li>
            </ul>
            <b>Note</b>: Currently there are two types of sessions supported in SAL endpoints. Namely HTTP transport based session which identifies the sessions based on HTTP cookies and the client session which identifies the session by looking at a SOAP header sent by the client with the `QName "[http://ws.apache.org/ns/synapse]ClientID"`.
         </td>
    </tr>
    <tr>
         <td>Session Timeout</td>
         <td>The number of milliseconds after which the session would time out.</td>
      </tr>
</table>

### Member Management Properties

Memeber properties can be used to associate configuration data with an endpoint.

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Host Name</td>
        <td></td>
    </tr>
    <tr>
        <td>HTTP Port</td>
        <td></td>
    </tr>
    <tr>
        <td>HTTPS Prot</td>
        <td></td>
    </tr>
</table>

### Miscellaneous Properties

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>URI</td>
        <td>
            EPR of the target endpoint. Following are the sample address URI definition.</br>
            <ul>
                <li><b>HTTP</b>: http://localhost:9000/services/SimpleStockQuoteService</li>
                <li><b>JMS</b>:
                    jms:/SimpleStockQuoteService?transport.jms.ConnectionFactoryJNDIName=QueueConnectionFactory&amp;java.naming.factory.initial=org.apache.activemq.jndi.ActiveMQInitialContextFactory&amp;java.naming.provider.url=tcp://localhost:61616&amp;transport.jms.DestinationType=topic
                </li>
                <li><b>Mail</b>: guest@host</li>
                <li><b>VFS</b>: vfs:file:///home/user/directory\ vfs:"&gt;file:///home/user/file\ vfs:</li>
                <li><b>FIX</b>: fix://host:port?BeginString=FIX4.4&amp;SenderCompID=WSO2&amp;TargetCompID=APACHE</li>
            </ul>
            If you want to define the URL with environment properties, you can define it as shown below.</br>
            <code>
                <?xml version="1.0" encoding="UTF-8"?> 
                <endpoint xmlns=" http://ws.apache.org/ns/synapse " name="JSON_EP"> 
                <address uri="$SYSTEM:VAR"/> 
                </endpoint>
            </code>
            Here <code>VAR</code> is the url you need to have set as environment property. This is useful when you need to need to deploy the endpoint in a container.
        </td>
    </tr>
    <tr>
        <td>Optimize</td>
        <td>
            Optimization for the message, which transfers binary data. The available values are as follows.
            <ul>
                <li>Leave As-Is: If this is selected, there will be no special optimization. The original message will be kept.</li>
                <li>SwA: If this is selected, the message is optimized as a SwA (SOAP with Attachment) message.</li>
                <li>MTOM: If this is selected, the message is optimized using a MTOM (message transmission optimization mechanism).</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td></td>
    </tr>
    <tr>
         <td>
            uri-template
         </td>
         <td>
            The URI template of the endpoint. Insert <code>uri.var.</code> before each variable. <b>Note</b>If the endpoint URL is an encoded URL, then you need to add <code>legacy-encoding:</code> when defining the uri-template. E.g., <code>uri-template="legacy-encoding:{uri.var.APIurl}"</code>.</br>
            The <a href="https://docs.wso2.com/enterprise-service-bus/Working+with+APIs#WorkingwithAPIs-URItemplates">URI template</a> that constructs the RESTful endpoint URL at runtime.
            <b>Note</b>: Using the URI postfix property: Let's take a look at it using an example. If you add a <code>/</code> between <code>{uri.var.context2}{uri.var.postfix}</code>, it is evaluated as an invalid invocation because <code> {uri.var.postfix}</code> contains a <code>/</code> at the start.</p>
               <p>Example:</p>
               <div class="code panel pdl" style="border-width: 1px;">
                  <div class="codeContent panelContent pdl">
                     <div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence">
                        <pre class="sourceCode java">
                            <code class="sourceCode java"><span id="cb1-1"><a href="#cb1-1"></a>&lt;http uri-template=<span class="st">&quot;http://{uri.var.host}:{uri.var.port}/{uri.var.context1}/services/{uri.var.context2}{uri.var.postfix}&quot;</span> method=<span class="st">&quot;get&quot;</span>&gt;</span></code>
                        </pre>
                     </div>
                  </div>
               </div>
            </div>
         </td>
      </tr>
      <tr>
         <td>HTTP Method</td>
         <td>
            <p>The HTTP method to use during the invocation of the endpoint. Supported methods are as follows.</p>
            <ul>
               <li>Get</li>
               <li>Post</li>
               <li>Patch</li>
               <li>Put</li>
               <li>Delete</li>
               <li>Options</li>
               <li>Head</li>
               <li>Leave-as-is</li>
            </ul>
         </td>
      </tr>
      <tr>
         <td>WSDL URI</td>
         <td>The URI of the WSDL. Click <strong>Test</strong> to test the URI.</td>
      </tr>
      <tr>
         <td>Service</td>
         <td>
            The service selected from the available services for the WSDL.</br>
            The `service` and `port` name containing the target EPR has to be specified with the `service` and `port` (or `endpoint`) attributes respectively.
         </td>
      </tr>
      <tr>
         <td>Port</td>
         <td>
            The port selected for the service specified in the <b>Service</b> parameter. In a WSDL, an endpoint is bound to each port inside each service. 
         </td>
      </tr>
</table>

Click **Add Property** to open the **Properties** tab and add the required properties.

<table>
   <thead>
      <tr>
         <th>Parameter Name</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>Name</td>
         <td>The name of the endpoint property.</td>
      </tr>
      <tr>
         <td>Value</td>
         <td>The value of the endpoint property.</td>
      </tr>
      <tr >
         <td>Scope</td>
         <td>
            The scope of the property. Possible values are as follows.
            <ul>
               <li>Default</li>
               <li>Transport</li>
               <li>Axis2</li>
               <li>axis2-client</li>
            </ul>
            <p>For more information about these scopes, see <a href="../references/mediators/accessing-Properties-with-XPath.md">XPath Extension Functions</a> .</p>
         </td>
      </tr>
   </tbody>
</table>

### Quality of Service Properties

QoS (Quality of Service) aspects such as WS-Security and WS-Addressing may be enabled on messages sent to an endpoint using `enableSec` and `enableAddressing` elements. Optionally, the WS-Security policies could be specified using the `policy` attribute.

<table>
    <tr>
        <th>Property</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>enableSec [policy="key"]</td>
        <td>
            This enables WS-Security for the message which is sent to the endpoint. The optional policy attribute specifies the WS-Security policy.
        </td>
    </tr>
    <tr>
        <td>enableAddressing [version="final | submission"] [seperateListener=" true | false"]</td>
        <td>
            This enables WS-Addressing for the message which is sent to the endpoint. User can specify to have separate listener with version final or submission.
        </td>
    </tr>
</table>

### Endpoint Error Handling Properties

#### Timeout Properties

<table>
   <thead>
      <tr class="header">
         <th>
            <p>Property</p>
         </th>
         <th>
            <p>Description</p>
         </th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <p>Timeout Action (responseAction)</p>
         </td>
         <td>
            <p>When a response comes to a timed out request, specifies whether to discard it or invoke the fault handler. If you select "never", the endpoint remains in the "Active" state. This parameter is used to specify the action to perform once an endpoint has timed out. The available options are as follows:</p>
            <ul>
               <li>Never: The endpoint will never time out. This is the default setting.</li>
               <li>Discard:  If this is selected, the responses which arrive after the endpoint has timed out will be discarded.</li>
               <li>Fault: If this is selected, a fault sequence is triggered when the endpoint is timed out.</li>
            </ul>
            <b>Note</b>: You can specify a value that is 1 millisecond less than the time duration you specify for the endpoint time out for the <code>synapse.timeout_handler_interval</code> property in the <code>EI_Home/conf/synapse.properties</code> file. This would minimise the number of late responses from the backend.
            </ul>
         </td>
      </tr>
      <tr>
         <td>
            <p>Timeout Duration</p>
         </td>
         <td>
            Connection timeout interval. If the remote endpoint does not respond in this time, it will be marked as "Timeout." This can be defined as a static value or as a **dynamic value**.</br>
            Miliseconds/ XPATH expression. Default value is 60000.
         </td>
      </tr>
    </tbody>
</table>

#### Suspend Endpoint

The `         markForSuspension        ` element contains the following
parameters which affect the suspension of a  endpoint which would be
timed out after a specified time duration.

<table>
   <thead>
      <tr class="header">
         <th>
            <p>Property</p>
         </th>
         <th>
            <p>Description</p>
         </th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <p>Suspend Error Codes (errorCodes)</p>
         </td>
         <td>
            Comma separated list of <a href="https://docs.wso2.com/display/EI650/Error+Handling#ErrorHandling-codes">error codes. 
            This parameter allows you to select one or more error codes from the List of Values. If any of the selected errors is received from the endpoint, the endpoint will be suspended. All the errors except the errors specified in <code>markForSuspension</code>.</br>
            Only these defined error codes will directly send the endpoint into the "Suspended" state . Any other error code, which is not specified under <code>MarkForSuspension</code> will keep the endpoint in the "Active" state without suspending.</br>
            If you do not specify these error codes, by default, a ll the errors except the errors specified in <code>markForSuspension</code> will suspend the endpoint.
         </td>
      </tr>
      <tr>
         <td>
            <p>Suspend Initial Duration (initialDuration)</p>
         </td>
         <td>
            The time duration (in mili seconds) for which the endpoint will be suspended, when one or more suspend error codes are received from it for the first time. After an endpoint gets "Suspended," it will wait for this amount of time before trying to send the messages coming to it. All the messages coming during this time period will result in fault sequence activation.</br>
            Default: 30000.
         </td>
      </tr>
      <tr>
         <td>
            <p>Suspend Maximum Duration</p>
         </td>
         <td>
            <p>The maximum time duration (Millis) for which the endpoint is suspended when suspend error codes are received from it.</p>
         </td>
      </tr>
      <tr>
         <td>
            <p>Suspend Progression Factor (progressionFactor)</p>
         </td>
         <td>
            The progression factor for the geometric series. See the above formula for a more detailed description. The duration to suspend can vary from the first time suspension to the subsequent time. The factor value decides the suspense duration variance between subsequent suspensions.</br>
            The endpoint will try to send the messages after the <code>initialDuration</code>. If it still fails, the next duration is calculated as:<code>Min(current suspension duration * progressionFactor, maximumDuration)</code>.</br>
            Default: 1.
         </td>
      </tr>
    </tbody>
</table>

#### Suspend Endpoint on Failure

Leaf endpoints(Address and WSDL) can be suspended if they are detected
as failed endpoints. When an endpoint is in in suspended state for a
specified time duration following a failure, it cannot process any new
messages. The following formula determines the wait time before the next
attempt.

`         next suspension time period = Max (Initial Suspension duration * (progression factor*        `
`                              try count                           `
`         *), Maximum Duration)        `

All the variables in the above formula are configuration values used to
calculate the try count. Try count is the number of tries carried out
after the endpoint is suspended. The increase in the try count causes an
increase in the next suspension time period. This time period is bound
to a maximum duration.

<table>
   <thead>
      <tr class="header">
         <th>
            <p>Property</p>
         </th>
         <th>
            <p>Description</p>
         </th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <p>Retry Error codes (errorCodes)</p>
         </td>
         <td>
            A (comma-separated) list of error codes. If these error codes are received from the endpoint, the request will be subjected to a timeout.</br>
            The defined error codes put the endpoint into the "Timeout" state marking it for suspension. After the number of defined <code>retriesBeforeSuspension</code> exceeds, the endpoint will be suspended.</br>
            Default: 101504, 101505.</br>
            See <a href="https://svn.apache.org/repos/asf/synapse/trunk/java/modules/core/src/main/java/org/apache/synapse/SynapseConstants.java">SynpaseConstant</a> class for a list of available error codes.
         </td>
      </tr>
      <tr>
         <td>
            <p>Retry Count (retriesBeforeSuspension)</p>
         </td>
         <td>
            The number of times the endpoint should be allowed to retry sending the response before it is marked for suspension. In the "Timeout" state this number of requests minus one can be tried and fail before the endpoint is marked as "Suspended". This setting is per endpoint, not per message, so several messages can be tried in parallel and fail and the remaining retries for that endpoint will be reduced. Default: 0.</br>
            <b>Note</b>: If you do not specify these error codes, or if you do not specify any error codes under <code>suspendOnFailure</code> , by default, the "HTTP Connection Closed" (i.e., 101504) and "HTTP Connection Timeout" (i.e., 101505) errors act as "Timeout" errors, and all other errors will put the endpoint into the "Suspended" state after retrying.
         </td>
      </tr>
      <tr>
         <td>
            <p>Retry Delay (retryDelay)</p>
         </td>
         <td>
            The time to wait between the last retry attempt and the next retry. Default: 0.
         </td>
      </tr>
    </tbody>
</table>

#### WS Addressing Properties

<table>
    <tbody>
      <tr>
         <td>
            <p>WS-Addressing</p>
         </td>
         <td>
            <p>Adds WS-Addressing headers to the endpoint.</p>
         </td>
      </tr>
      <tr class="odd">
         <td>
            <p>Separate Listener</p>
         </td>
         <td>
            <p>The listener to the response will be a separate transport stream from the caller.</p>
         </td>
      </tr>
      <tr class="even">
         <td>
            <p>WS-Security</p>
         </td>
         <td>
            <p>Adds WS-Security features as described in a policy key (referring to a registry location).</p>
         </td>
      </tr>
      <tr class="odd">
         <td>Non Retry Error Codes</td>
         <td>
            <p>When a child endpoint of a <a href="_Configuring_Failover_Endpoints_">failover endpoint</a> or <a href="_Load-balance_Group_">load-balance endpoint</a> fails for one of the error codes specified here, the child endpoint will be marked for suspension and the request will not be sent to the next endpoint in the group.</p>
         </td>
      </tr>
      <tr class="even">
         <td>Retry Error Codes</td>
         <td>When adding a child endpoint to a <a href="_Configuring_Failover_Endpoints_">failover endpoint</a> or <a href="_Load-balance_Group_">load-balance endpoint</a> , you can specify the error codes that trigger this node to be <a href="Endpoint-Error-Handling_119131815.html#EndpointErrorHandling-retryConfig">retried</a> instead of suspended when that error is encountered. This is useful when you know that certain errors are transient and that the node will become available again shortly. Note that if you specify an error code as a Retry code on one node in the group but specify that same code as a Non Retry error code on another node in the group, it will be treated as a Non Retry error code for all nodes in the group.</td>
      </tr>
   </tbody>
</table>

## Examples
..

## Guides
