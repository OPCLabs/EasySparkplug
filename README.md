# Rapid Toolkit for Sparkplug
<a href="https://www.opclabs.com/products/quickopc"><img align="right" src="Image-Product-RapidToolkitForSparkplug-Web.png"></a>
- NuGet package: 
[**OpcLabs.EasySparkplug**](https://www.nuget.org/packages/OpcLabs.EasySparkplug)

Sparkplug is a trademark of Eclipse Foundation, Inc. "MQTT" is a trademark of
the OASIS Open standards consortium. Other related terms are trademarks of 
their respective owners. Any use of these terms on this site is for 
descriptive purposes only and does not imply any sponsorship, endorsement or 
affiliation.

Rapid Toolkit for Sparkplug allows rapid Sparkplug application and edge node 
development. Supports Sparkplug A and B. It allows you to create Sparkplug 
software with minimal effort, and without having to deal with the underlying 
MQTT protocol and the Sparkplug encoding and messaging rules.

Rapid Toolkit for Sparkplug is a commercially licensed product. Without a 
license key, it runs in a trial mode. The trial provides valid edge node or 
host application data for 30 minutes; after that period, the component (your 
app) needs to be re-started, and so on. You must also comply with licensing 
terms for 3rd-party material redistributed with Rapid Toolkit for Sparkplug. 
For details, see the documentation.

| Ready to purchase? See [full price list](https://www.opclabs.com/purchase/full-price-list). |
| ------------------------------------------------------------------------------------------- |

Remember that NuGet packages are primarily a tool for resolving 
build-time dependencies. The amount of functionality that you get through 
Rapid Toolkit for Sparkplug NuGet packages is smaller than what the toolkit 
can actually do for you. If you want a full coverage of the features, you 
would be better off downloading the Setup program from 
[OPC Labs Web site](https://www.opclabs.com). Further below you will find a 
list of differences between the two distribution forms.

Rapid Toolkit for Sparkplug requires **.NET Framework** 4.7.2 or **.NET** 8.0 
as a minimum. Under .NET 8.0+, it is supported on **Linux**, **macOS** and 
**Microsoft Windows**. 

PLEASE DO NOT USE PRE-RELEASE PACKAGES UNLESS INSTRUCTED TO DO SO.

Need help, tech support, or missing some example? Ask us for it on our 
[Online Forums](https://www.opclabs.com/forum/index)! You do not have to own 
a commercial license in order to use Online Forums, and we reply to every 
post.

What is included in the NuGet packages
--------------------------------------
- Runtime assemblies for all programming models.
- IntelliSense support (XML comments).

What is only available from the [Setup program](https://www.opclabs.com/download)
---------------------------------------------
- Complete set of Examples and Demo applications.

What is only available from the [Setup program](https://www.opclabs.com/download) or the Web site
-------------------------------------------------------------
[Knowledge Base link - Tool Downloads](https://kb.opclabs.com/Tool_Downloads)
- Various tools, such as Launcher, Sparkplug Demo Edge Node, SparkplugCmd Utility.
- License Manager (GUI or console-based) utility.

How to start
------------
If you do not mind reading the documentation: [Getting Started with Rapid Toolkit for Sparkplug](
https://opclabs.doc-that.com/files/onlinedocs/OPCLabs-ConnectivityStudio/Latest/User%27s%20Guide%20and%20Reference-OPC%20Studio/webframe.html#Getting%20Started%20with%20EasySparkplug.html).
Or, the whole [User's Guide](https://www.opclabs.com/documentation).

Otherwise, just instantiate one of the following objects, and explore its methods:

- `OpcLabs.EasySparkplug.EasySparkplugConsumer` (for developing Sparkplug host applications)
- `OpcLabs.EasySparkplug.EasySparkplugEdgeNode` (for developing Sparkplug edge nodes)

Example code for Sparkplug edge node
------------------------------------
C#:
```csharp
using OpcLabs.EasySparkplug;
...

// Note that the default port for the "mqtt" scheme is 1883.
var hostDescriptor = new SparkplugHostDescriptor("mqtt://localhost");

// Instantiate the edge node object.
var edgeNode = new EasySparkplugEdgeNode(hostDescriptor, "easyGroup", "easySparkplugDemo");

// Define a metric providing random integers.
var random = new Random();
edgeNode.Metrics.Add(new SparkplugMetric("MyMetric").ReadValueFunction(() => random.Next()));

// Start the edge node.
edgeNode.Start();
```

Example code for Sparkplug host application
-------------------------------------------
C#:
```csharp
using OpcLabs.EasySparkplug;
...

// Note that the default port for the "mqtt" scheme is 1883.
var hostDescriptor = new SparkplugHostDescriptor("mqtt://localhost");

// Instantiate the consumer object.
var consumer = new EasySparkplugConsumer();

Console.WriteLine("Subscribing...");
// The callback is a lambda expression the displays the value
// In this example, we specify the precise Sparkplug group ID, edge node ID, and metric name.
consumer.SubscribeEdgeNodeMetric(hostDescriptor, 
    "easyGroup", "easySparkplugDemo", "Random",
    (sender, eventArgs) =>
    {
        if (eventArgs.Succeeded)
        {
            if (eventArgs.HasData)
                Console.WriteLine("Value: {0}", eventArgs.MetricData.Value);
        }
        else
            Console.WriteLine("*** Failure: {0}", eventArgs.ErrorMessageBrief);
    });
```

Examples on GitHub
------------------
As opposed to the sample NuGet packages, the examples on GitHub also include 
Web, Windows Forms, Windows Service and WPF projects.

- In C#: https://github.com/OPCLabs/Examples-ConnectivityStudio-CSharp.
- In VB.NET: https://github.com/OPCLabs/Examples-ConnectivityStudio-VBNET.

***
