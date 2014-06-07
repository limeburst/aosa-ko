# Telepathy

# Telepathy

Telepathy is a modular framework for real-time communications that handles voice, video, text, file transfer, and so on. What's unique about Telepathy is not that it abstracts the details of various instant messaging protocols, but that it provides the idea of communications as a service, in much the same way that printing is a service, available to many applications at once. To achieve this Telepathy makes extensive use of the D-Bus messaging bus and a modular design.

Telepathy는 음성, 영상, 텍스트, 파일 전송 등 실시간 커뮤니케이션을 위한 모듈화된 프레임워크입니다. Telepathy가 특별한 점은, 다양한 인스턴트 메시징 프로토콜의 세부 사항을 추상화할 뿐만이 아니라, 커뮤니케이션을 다수의 응용 프로그램에게 동시에 사용 가능한 프린팅처럼 하나의 서비스의 개념으로 제공한다는 것입니다. Telepathy는 이러한 점을 달성하기 위해 D-Bus 메시징 버스와 모듈화된 설계를 광범위하게 사용합니다.

Communications as a service is incredibly useful, because it allows us to break communications out of a single application. This enables lots of interesting use cases: being able to see a contact's presence in your email application; start communicating with her; launching a file transfer to a contact straight from your file browser; or providing contact-to-contact collaboration within applications, known in Telepathy as Tubes.

서비스로서의 커뮤니케이션은, 단일 프로그램에서만의 커뮤니케이션에서 탈피할 수 있게 해주므로 굉장히 유용합니다. 이 점은, 이메일 클라이언트에서 연락처의 부재 여부를 확인하고, 그와 커뮤니케이션을 시작하고, 파일 브라우저에서 바로 파일 전송을 하거나, Telepathy에서 Tubes로 알려진 기능인, 프로그램 내에서 연락처 간의 협업 기능의 제공 등, 많은 흥미로운 사용례를 가능하게 만들어 줍니다. 

Telepathy was created by Robert McQueen in 2005 and since that time has been developed and maintained by several companies and individual contributors including Collabora, the company co-founded by McQueen.

Telepathy는 2005년도에 로버트 맥퀸에 의해 만들어졌으며, 그 이후로 맥퀸이 공동 창립한 회사인 Collabora를 포함하여 여러 회사와 개인에 의해 개발, 유지되고 있습니다.

> The D-Bus Message Bus

> D-Bus 메시지 버스

> > D-Bus is an asynchronous message bus for interprocess communication that forms the backbone of most GNU/Linux systems including the GNOME and KDE desktop environments. D-Bus is a primarily a shared bus architecture: applications connect to a bus (identified by a socket address) and can either transmit a targeted message to another application on the bus, or broadcast a signal to all bus members. Applications on the bus have a bus address, similar to an IP address, and can claim a number of well-known names, like DNS names, for example `org.freedesktop.Telepathy.AccountManager`. All processes communicate via the D-Bus daemon, which handles message passing, and name registration.

> > D-Bus는 GNOME, KDE 데스크톱 환경을 포함한 대부분의 GNU/Linux 시스템의 백본을 구성하는 프로세스 간 커뮤니케이션을 위한 비동기적인 메시지 버스입니다. D-Bus는 공유 버스 설계를 주로 합니다. 응용 프로그램들은 (소켓 주소로 구분되는) 버스에 연결하여 버스에 연결된 다른 응용 프로그램을 대상으로 메시지를 보내거나 모든 버스 구성원에게 브로드캐스트 신호를 보낼 수 있습니다. 버스에 연결된 응용 프로그램에게는 IP 주소와 유사한 버스 주소가 있으며, `org.freedesktop.Telepathy.AccountManager` 등, DNS 이름처럼 다수의 잘 알려진 이름을 차지할 수 있습니다. 모든 프로세스는 메시지 전달과 이름 등록을 처리하는 D-Bus 데몬을 통해 통신합니다.

> > From the user's perspective, there are two buses available on every system. The system bus is a bus that allows the user to communicate with system-wide components (printers, bluetooth, hardware management, etc.) and is shared by all users on the system. The session bus is unique to that user—i.e., there is a session bus per logged-in user—and is used for the user's applications to communicate with each other. When a lot of traffic is to be transmitted over the bus, it's also possible for applications to create their own private bus, or to create a peer-to-peer, unarbitrated bus with no `dbus-daemon`.

> > 사용자의 관점에서 볼 때, 모든 시스템에는 사용 가능한 두 개의 버스가 있습니다. 시스템 버스는 사용자가 시스템 전체에 걸쳐 있는 구성 요소(프린터, 블루투스, 하드웨어 관리 등)들과 통신하게 해 주며, 해당 시스템을 사용하는 모든 사용자와 공유됩니다. 세션 버스는 사용자에게 유일하며, 즉, 로그인된 사용자당 하나의 세션 버스가 있으며, 사용자의 응용 프로그램 간의 통신을 위해 사용됩니다. 대량의 트래픽이 버스를 통해 전달되어야 할 경우, 응용 프로그램들은 사설 버스나, 중재자인 `dbus-daemon`이 없는 P2P 버스를 생성하여 통신할 수도 있습니다.

> > Several libraries implement the D-Bus protocol and can communicate with the D-Bus daemon, including libdbus, GDBus, QtDBus, and python-dbus. These libraries are responsible for sending and receiving D-Bus messages, marshalling types from the language's type system into D-Bus' type format and publishing objects on the bus. Usually, the libraries also provide convenience APIs for listing connected applications and activatable applications, and requesting well-known names on the bus. At the D-Bus level, all of these are done by making method calls on an object published by dbus-daemon itself.

> > libdus, GDBus, QtDBus, python-dbus 등 다수의 라이브러리가 D-Bus 데몬과 통신할 수 있는 D-Bus 프로토콜을 구현합니다. 이 라이브러리들은 D-Bus 메시지를 송수신하고, 언어의 타입 시스템을 D-Bus의 타입 형식으로 마샬링하고, 객체를 버스에 발행하는 역할을 합니다. 이러한 라이브러리들은 주로, 연결됐거나 활성화 가능한 응용 프로그램들의 목록을 받아오거나, 버스에서 잘 알려진 이름들을 요청하는 편의성 API도 제공합니다.

> > For more information on D-Bus, see [http://www.freedesktop.org/wiki/Software/dbus](http://www.freedesktop.org/wiki/Software/dbus).

> > D-Bus에 대해 더 알아보고 싶으시다면, [http://www.freedesktop.org/wiki/Software/dbus](http://www.freedesktop.org/wiki/Software/dbus)를 보세요.

## 20.1. Components of the Telepathy Framework

## 20.1. Telepathy 프레임워크의 구성 요소

Telepathy is modular, with each module communicating with the others via a D-Bus messaging bus. Most usually via the user's session bus. This communication is detailed in the Telepathy specification. The components of the Telepathy framework are as shown in Figure 20.1:

Telepathy는 모듈식이며, 모듈들은 서로간 D-Bus 메시징 버스를 통해 통신합니다. 대부분의 모듈들은 사용자의 세션 버스를 사용합니다. 이 커뮤니케이션은 Telepathy 명세에 상세히 설명되어 있습니다. 그림 20.1에 Telepathy 프레임워크의 구성 요소들이 나와 있습니다.

![Telepathy 구성 요소 예시](http://aosabook.org/images/telepathy/telepathy-components.png)

* A Connection Manager provides the interface between Telepathy and the individual communication services. For instance, there is a Connection Manager for XMPP, one for SIP, one for IRC, and so on. Adding support for a new protocol to Telepathy is simply a matter of writing a new Connection Manager.
* The Account Manager service is responsible for storing the user's communications accounts and establishing a connection to each account via the appropriate Connection Manager when requested.
* The Channel Dispatcher's role is to listen for incoming channels signalled by each Connection Manager and dispatch them to clients that indicate their ability to handle that type of channel, such as text, voice, video, file transfer, tubes. The Channel Dispatcher also provides a service so that applications, most importantly applications that are not Telepathy clients, can request outgoing channels and have them handled locally by the appropriate client. This allows an application, such as an email application, to request a text chat with a contact, and have your IM client show a chat window.
* Telepathy clients handle or observe communications channels. They include both user interfaces like IM and VoIP clients and services such the chat logger. Clients register themselves with the Channel Dispatcher, giving a list of channel types they wish to handle or observe.

* Connection Manager는 Telepathy와 커뮤니케이션 서비스 하나 하나와의 인터페이스를 제공합니다. 예를 들어, XMPP를 위한 Connection Manager가 있으며, SIP, IRC 등을 위한 Connection Manager가 하나씩 있습니다. 새로운 프로토콜에 대한 지원을 추가하는 것은 새로운 Connection Manager를 작성하면 되는 문제입니다. Account Manager 서비스는 사용자의 커뮤니케이션 계정들과 각 계정을 요청이 들어왔을 때 적합한 Connection Manager에 연결되는 역할을 합니다.
* Account Manager 서비스는 사용자의 커뮤니케이션 계정을 저장하고, 요청을 받았을 때 적합한 Connection Manager를 통해 연결하는 역할을 합니다.
* Channel Dispatcher는 각 Connection Manager로부터. Channel Dispatcher는, 특히 Telepathy 클라이언트가 아닌 응용 프로그램이, 발송 채널을 요청하고, 적절한 클라이언트가 그것을 지역적으로 처리할 수 있게 합니다. 이것은 응용 프로그램이, 예를 들어 이메일 클라이언트가 연락처와의 텍스트 채팅을 요청하면, 인스턴스 메시징 클라이언트가 채팅 창을 보여주게 만들 수 있습니다.
* Telepathy 클라이언트는 커뮤니케이션 채널을 처리하거나 관찰합니다. 클라이언트는 인스턴스 메신저, VoIP 클라이언트 등 사용자 인터페이스와, 대화 로거 등의 서비스를 포함합니다. 클라이언트는 처리하거나 관찰하고자 하는 채널 종류의 목록을 전달하며 자신을 Channel Dispatcher에 등록합니다.

Within the current implementation of Telepathy, the Account Manager and the Channel Dispatcher are both provided by a single process known as Mission Control.

현재 Telepathy 구현에서, Account Manager와 Channel Dispatcher는 Mission Control이라는 하나의 프로세스가 제공합니다.

This modular design was based on Doug McIlroy's philosophy, "Write programs that do one thing and do it well," and has several important advantages:

이러한 모듈화 설계는, 더그 맥일로이의 철학인 "단 한 가지 일만을 훌륭하게 처리하는 프로그램을 작성하라" 에 기반하였고, 몇 가지 중요한 이점을 가집니다:

* Robustness: a fault in one component won't crash the entire service.
* Ease of development: components can be replaced within a running system without affecting others. It's possible to test a development version of one module against another known to be good.
* Language independence: components can be written in any language that has a D-Bus binding. If the best implementation of a given communications protocol is in a certain language, you are able to write your Connection Manager in that language, and still have it available to all Telepathy clients. Similarly, if you wish to develop your user interface in a certain language, you have access to all available protocols.
* License independence: components can be under different software licenses that would be incompatible if everything was running as one process.
* Interface independence: multiple user interfaces can be developed on top of the same Telepathy components. This allows native interfaces for desktop environments and hardware devices (e.g., GNOME, KDE, Meego, Sugar).
* Security: Components run in separate address spaces and with very limited privileges. For example, a typical Connection Manager only needs access to the network and the D-Bus session bus, making it possible to use something like SELinux to limit what a component can access.

* 견고함: 단일 요소의 결함은 전체 서비스를 무너지게 하지 않습니다.
* 개발의 편리함: 구성 요소들은 동작 중인 시스템 내에서 다른 구성 요소에 영향을 주지 않으면서 교체될 수 있습니다. 개발 중인 모듈을 안정된 버전의 모듈과 비교하며 테스트할 수도 있습니다.
* 언어 독립성: 구성 요소들은 D-Bus 바인딩이 있는 어떠한 언어로도 작성될 수 있습니다. 주어진 커뮤니케이션 프로토콜의 가장 좋은 구현체가 특정 언어로 작성되었다면, 그 언어로 Connection Manager를 작성할 수 있으며, 모든 Telepathy 클라이언트에서 사용될 수 있습니다. 비슷한 맥락에서, 어떠한 언어로 사용자 인터페이스를 개발하더라도 모든 프로토콜을 이용할 수 있습니다.
* 라이센스 독립성: 시스템이 하나의 프로세스로 동작한다면 라이센스가 호환되지 않았겠지만, 서로 별개인 구성 요소로 이루어져 있기 때문에 구성 요소들은 서로 다른 소프트웨어 라이센스를 가질 수 있습니다.
* 인터페이스 독립성: 같은 Telepathy 구성 요소 위에서 다양한 사용자 인터페이스를 개발할 수 있습니다. 이것은 데스크톱 환경과 하드웨어 장치를 위한 네이티브 인터페이스를 가능하게 합니다. (GNOME, KDE, Meego, Sugar 등).
* 보안: 구성 요소들은 각각의 주소공간에서 제한된 권한을 가지고 실행됩니다. 예를 들어, 전형적인 Connection Manager는 네트워크와 D-Bus 세션 버스에 대한 접근 권한만 필요로 하며, SELinux 같은 프로그램을 사용하여 구성 요소의 자원 접근 권한을 제한할 수 있습니다.

The Connection Manager manages a number of Connections, where each Connection represents a logical connection to a communications service. There is one Connection per configured account. A Connection will contain multiple Channels. Channels are the mechanism through which communications are carried out. A channel might be an IM conversation, voice or video call, file transfer or some other stateful operation. Connections and channels are discussed in detail in Section 20.3.

Connection Manager는 여러 개의 Connection을 관리하며, 각 Connection은 커뮤니케이션 장치와의 논리적인 연결을 나타냅니다. 설정된 계정 하나당 하나의 Connection이 존재하며, 하나의 Connection은 커뮤니케이션이 이루어지는 작동 메커니즘인, Channel을 여러 개 포함합니다. Channel은 인스턴스 메신저 대화, 음성, 영상 통화, 파일 전송, 혹은 다른 상태 유지 작업일 수 있습니다. Connection과 Channel에 대해서는 20.3. 에서 자세히 다뤄집니다.

## 20.2. How Telepathy uses D-Bus

## 20.2. Telepathy가 D-Bus를 사용하는 방식

Telepathy components communicate via a D-Bus messaging bus, which is usually the user's session bus. D-Bus provides features common to many IPC systems: each service publishes objects which have a strictly namespaced object path, like `/org/freedesktop/Telepathy/AccountManager3`. Each object implements a number of interfaces. Again strictly namespaced, these have forms like `org.freedesktop.DBus.Properties and ofdT.Connection`. Each interface provides methods, signals and properties that you can call, listen to, or request.

Telepathy 구성 요소들은 D-Bus 메시징 버스를 통해 통신하며, 주로 사용자의 세션 버스를 사용합니다. D-Bus는 많은 IPC 시스템에서 공통으로 찾아볼 수 있는 기능을 제공합니다. 서비스는 `/org/freedesktop/Telepathy/AccountManager3`처럼, 엄격히 정해진 이름공간의 객체 경로를 가진 객체를 발행하며, 각 객체는 몇 가지 인터페이스를 구현합니다. 이들 역시 `org.freedesktop.DBus.Properties and ofdT.Connection` 같은 형식의 엄격한 이름공간을 가지며, 인터페이스는 호출, 듣기, 또는 요청 가능한 메서드, 시그널, 그리고 속성을 제공합니다.

![D-Bus 서비스가 발행한 객체들의 개념적 표현](http://aosabook.org/images/telepathy/bus-hierarchy-conceptual.png)

> Publishing D-Bus Objects

> D-Bus 객체 발행하기

> > Publishing D-Bus objects is handled entirely by the D-Bus library being used. In effect it is a mapping from a D-Bus object path to the software object implementing those interfaces. The paths of objects being published by a service are exposed by the optional `org.freedesktop.DBus.Introspectable` interface.

> > D-Bus 객체 발행은 사용하는 온전히 D-Bus 라이브러리에 의해 처리됩니다. 결과적으로 볼 때, 객체 발행은 D-Bus 객체 경로를, 해당하는 인터페이스를 구현하는 소프트웨어 객체로 대응시키는 것입니다. 서비스가 발행하는 객체의 경로는 `org.freedesktop.DBus.Introspectable`이라는 선택적인 인터페이스에 의해 노출됩니다.

> > When a service receives an incoming method call with a given destination path (e.g., `/ofdT/AccountManager`), the D-Bus library is responsible for locating the software object providing that D-Bus object and then making the appropriate method call on that object.

> > 서비스가 `/ofdT/AccountManager`와 같이 지정된 목적지 경로를 가진 메서드 호출을 받으면, D-Bus 라이브러리는 해당하는 D-Bus 객체를 제공하는 소프트웨어 객체를 찾고, 찾은 객체에 대한 올바른 메서드 호출을 하는 역할을 합니다.

The interfaces, methods, signal and properties provided by Telepathy are detailed in an XML-based D-Bus IDL that has been expanded to include more information. The specification can be parsed to generate documentation and language bindings.

Telepathy가 제공하는 인터페이스, 메서드, 시그널, 속성들은, 더 많은 정보를 포함하기 위해 확장된, XML 기반의 D-Bus IDL로 명시되어 있습니다. 이 명세는 구문 분석 되어 문서와 언어 바인딩을 생성할 수 있습니다.

Telepathy services publish a number of objects onto the bus. Mission Control publishes objects for the Account Manager and Channel Dispatcher so that their services can be accessed. Clients publish a Client object that can be accessed by the Channel Dispatcher. Finally, Connection Managers publish a number of objects: a service object that can be used by the Account Manager to request new connections, an object per open connection, and an object per open channel.

Telepathy 서비스들은 버스에 몇 가지 객체를 발행할 수 있습니다. Mission Control은 Account Manager와 Channel Dispatcher의 서비스에 접근하기 위한 객체를, 클라이언트는 Channel Dispatcher가 접근 가능한 Client 객체를, 그리고 마지막으로 Connection Manager는, Account Manager가 새로운 연결을 요청하기 위해 사용하는 서비스 객체, 열린 연결당 하나의 객체, 그리고 열린 채널당 하나의 객체를 발행할 수 있습니다.

Although D-Bus objects do not have a type (only interfaces), Telepathy simulates types several ways. The object's path tells us whether the object is a connection, channel, client, and so on, though generally you already know this when you request a proxy to it. Each object implements the base interface for that type, e.g., `ofdT.Connection `or `ofdT.Channel`. For channels this is sort of like an abstract base class. Channel objects then have a concrete class defining their channel type. Again, this is represented by a D-Bus interface. The channel type can be learned by reading the `ChannelType` property on the Channel interface.

D-Bus 객체는 타입이 없지만(인터페이스만 있음) Telepathy는 몇 가지 방법으로 타입을 가장합니다. 객체의 경로는, 이미 프락시를 요청 할 때 알 수 있지만, 객체가 연결인지, 채널인지, 클라이언트인지 등의 정보를 알려줍니다. 각 객체는 `ofdT.Connection `또는 `ofdT.Channel`처럼 해당되는 타입의 기초 인터페이스를 구현합니다. 이 인터페이스는 채널에겐 추상화된 기반 클래스와 비슷합니다. 이제 채널 객체는 채널 타입을 정의하는 구상 클래스를 가지며, 이 역시 D-Bus 인터페이스에 의해 표현됩니다. 채널 타입은 Channel 인터페이스의 `ChannelType` 속성을 읽음으로서 알 수 있습니다.

Finally, each object implements a number of optional interfaces (unsurprisingly also represented as D-Bus interfaces), which depend on the capabilities of the protocol and the Connection Manager. The interfaces available on a given object are available via the `Interfaces` property on the object's base class.

마지막으로, 각 객체는 프로토콜과 Connection Manager의 기능에 의존하는 몇 가지 선택적인 인터페이스를 구현합니다(이 역시 D-Bus 인터페이스에 의해 표현됩니다). 주어진 객체 위에서 제공되는 인터페이스는 객체의 기반 클래스의 `Interface` 속성을 통해 사용할 수 있습니다.

For Connection objects of type `ofdT.Connection`, the optional interfaces have names like `ofdT.Connection.Interface.Avatars` (if the protocol has a concept of avatars), `odfT.Connection.Interface.ContactList` (if the protocol provides a contact roster—not all do) and `odfT.Connection.Interface.Location` (if a protocol provides geolocation information). For Channel objects, of type `ofdT.Channel`, the concrete classes have interface names of the form `ofdT.Channel.Type.Text`, `odfT.Channel.Type.Call` and `odfT.Channel.Type.FileTransfer`. Like Connections, optional interface have names likes `odfT.Channel.Interface.Messages` (if this channel can send and receive text messages) and `odfT.Channel.Interface.Group` (if this channel is to a group containing multiple contacts, e.g., a multi-user chat). So, for example, a text channel implements at least the `ofdT.Channel`, `ofdT.Channel.Type.Text` and `Channel.Interface.Messages` interfaces. If it's a multi-user chat, it will also implement `odfT.Channel.Interface.Group`.

`ofdT.Connection` 타입을 가진 Connection 객체의 선택적 인터페이스는 `ofdT.Connection.Interface.Avatars` (프로토콜에 아바타라는 개념이 있으면), `odfT.Connection.Interface.ContactList` (프로토콜이 연락처 목록을 제공한다면(모든 프로토콜이 제공하지는 않습니다)) and `odfT.Connection.Interface.Location` (프로토콜이 위치 정보를 제공하면) 과 같은 이름을 가집니다. `ofdT.Channel` 타입을 가진 Channel 객체의 구상 클래스는 `ofdT.Channel.Type.Text`, `odfT.Channel.Type.Call` 그리고 `odfT.Channel.Type.FileTransfer`의 형식의 인터페이스 이름을 가집니다. Connection과 비슷하게, 선택적 인터페이스는 `odfT.Channel.Interface.Messages` (채널이 문자 메시지를 송수신 할 수 있으면), 그리고 `odfT.Channel.Interface.Group` (채널이 다수의 연락처를 포함하는 그룹을 대상으로 하면, 예를 들어, 단체 채팅방) 과 같은 이름을 가집니다. 예를 들면, 문자 채널은 최소한 `ofdT.Channel`, `ofdT.Channel.Type.Text`, 그리고 `Channel.Interface.Messages` 인터페이스를 구현합니다. 단체 채팅방일 경우 `odfT.Channel.Interface.Group` 도 구현합니다.

> Why an Interfaces Property and not D-Bus Introspection?

> 왜 D-Bus 인트로스펙션이 있는데 Interface 속성을 사용하나요?

> > You might wonder why each base class implements an `Interfaces` property, instead of relying on D-Bus' introspection capabilities to tell us what interfaces are available. The answer is that different channel and connection objects may offer different interfaces to each other, depending on the capabilities of the channel or connection, but that most of the implementations of D-Bus introspection assume that all objects of the same object class will have the same interfaces. For example, in `telepathy-glib`, the D-Bus interfaces listed by D-Bus introspection are retrieved from the object interfaces a class implements, which is statically defined at compile time. We work around this by having D-Bus introspection provide data for all the interfaces that could exist on an object, and use the `Interfaces` property to indicate which ones actually do.

> > 왜 각 기반 클래스가, 사용 가능한 인터페이스들을 알려주는 D-Bus의 인트로스펙션 기능을 사용하지 않고 `Interfaces` 속성을 구현하는지 궁금하실 수도 있습니다. 그 이유는 서로 다른 채널과 커넥션 객체들은 가지는 기능에 따라 서로 다른 인터페이스를 가질 수 있지만, 대부분의 D-Bus 인트로스펙션 구현체들은 같은 객체 클래스의 모든 객체는 같은 인터페이스를 가진다고 가정하기 때문입니다. 예를 들어 `telepathy-glib`에선, D-Bus 인트로스펙션이 나열한 D-Bus 인터페이스들은 컴파일 타임에 정적으로 정의된 클래스가 구현하는 인터페이스들로부터 가져옵니다. 우리는 이 문제를 D-Bus 인트로스펙션에서 객체에 있을 수 있는 모든 인터페이스에 대한 정보를 제공하게 하고, `Interfaces` 속성이 실제로 객체가 가진 인터페이스를 정의하게 하여 회피합니다.

Although D-Bus itself provides no sanity checking that connection objects only have connection-related interfaces and so forth (since D-Bus has no concept of types, only arbitrarily named interfaces), we can use the information contained within the Telepathy specification to provide sanity checking within the Telepathy language bindings.

D-Bus 자체는 커넥션 객체가 커넥션과 관련된 인터페이스만 가지는지(D-Bus에는 임의의 기명 인터페이스만 있고 자료형에 대한 개념은 존재하지 않기 때문에) 따위에 대한 온전성을 확인해 주지 않지만, Telepathy 언어 바인딩 내 Telepathy 명세에 있는 정보를 사용하여 온전성 검사를 할 수 있습니다.

> Why and How the Specification IDL was Expanded

> IDL 명세가 왜, 어떻게 확장되었는가에 대해

> > The existing D-Bus specification IDL defines the names, arguments, access restrictions and D-Bus type signatures of methods, properties and signals. It provides no support for documentation, binding hints or named types.

> > 기존 D-Bus IDL 명세는 이름, 파라미터, 접근 제한, 메서드의 D-Bus 타입 시그니쳐, 속성, 그리고 시그널을 정의하지만, 문서, 바인딩 힌트, 기명 타입은 지원하지 않습니다.

> > To resolve these limitations, a new XML namespace was added to provide the required information. This namespace was designed to be generic so that it could be used by other D-Bus APIs. New elements were added to include inline documentation, rationales, introduction and deprecation versions and potential exceptions from methods.

> > 이러한 한계를 극복하기 위해, 필요한 정보를 제공하기 위한 새로운 XML 이름공간이 추가되었습니다. 이 이름공간은 제네릭 하게, 다른 D-Bus API들이 사용할 수 있도록 설계되었습니다. 인라인 문서, 근거, 서론, 대체된 버전들, 그리고 메서드에서 발생할 수 있는 예외를 포함하기 위한 엘리먼트들이 추가되었습니다.

> > D-Bus type signatures are the low-level type notation of what is serialized over the bus. A D-Bus type signature may look like (ii) (which is a structure containing two int32s), or it may be more complex. For example, `a{sa(usuu)}`, is a map from string to an array of structures containing uint32, string, uint32, uint32 (Figure 20.3). These types, while descriptive of the data format, provide no semantic meaning to the information contained in the type.

> > D-Bus 타입 시그니쳐는 버스 위에서 직렬화된 것들의 로우 레벨 타입 표기입니다. D-Bus 타입 시그니쳐는 `(ii)`(두개의 int32를 포함하는 구조체) 처럼 생겼거나, 더 복잡할 수도 있습니다. 예를 들어, `a{sa(usuu)}`는 uint32, string, uint32, uint32를 포함하는 구조체의 배열로 매핑된 string의 맵입니다(그림 20.3). 이 타입들은, 데이터 형식에 관해서 기술하지만, 타입에 저장된 정보에 대한 의미는 전혀 제공하지 않습니다.

> > In an effort to provide semantic clarity for programmers and strengthen the typing for language bindings, new elements were added to name simple types, structs, maps, enums, and flags, providing their type signature, as well as documentation. Elements were also added in order to simulate object inheritance for D-Bus objects.

> > 프로그래머들에게 의미론적 명료함을 제공하고 언어 바인딩을 위한 타이핑을 강화하기 위해 문서는 물론 간단한 타입, 구조체, 맵, 열거형, 플래그의 타입 시그니쳐를 제공하고, 들에 이름을 붙이기 위해, 새로운 엘리먼트들이 추가되었습니다.

![D-Bus 타입 (ii)와 a{sa(usuu)}](http://aosabook.org/images/telepathy/telepathy-types-unpacked.png)
