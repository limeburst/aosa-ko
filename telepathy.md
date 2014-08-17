# Telepathy

Telepathy는 음성, 영상, 텍스트, 파일 전송 등을 다루는 실시간 통신을 위한 모듈화된 프레임워크입니다. Telepathy의 차별점은 다양한 인스턴트 메시지 프로토콜의 세부 사항을 추상화 한다는 점이 아니라, 여러 응용 프로그램들이 동시에 사용 가능한 프린터 서비스처럼, 통신을 하나의 서비스로써 제공한다는 점입니다. Telepathy는 이것을 달성하기 위해 D-Bus 메시지 버스와 모듈화된 설계를 광범위하게 사용합니다.

서비스로서의 통신은 응용 프로그램 간의 통신 수단을 제공하므로 굉장히 유용합니다. 서비스로서의 통신은, 이메일 클라이언트에서 연락처의 부재 여부를 확인하고, 해당 연락처와 통신을 시작하고, 파일 브라우저에서 바로 파일을 전송하거나, Telepathy에서 Tubes로 알려진 기능인 응용 프로그램 내에서 연락처 간의 협업 기능의 제공 등, 많은 흥미로운 사용례를 가능하게 합니다. 

Telepathy는 2005년도에 로버트 맥퀸에 의해 만들어졌으며, 그 이후 맥퀸이 공동 창립한 회사인 Collabora를 포함한 여러 회사와 개인에 의해 유지, 개발되고 있습니다.

> D-Bus 메시지 버스

> D-Bus는 GNOME, KDE 데스크톱 환경 등, GNU/Linux 시스템의 백본 대부분을 구성하는, 프로세스 간 통신을 위한 비동기적 메시지 버스입니다. D-Bus의 설계는 공유 버스를 기반으로 합니다. 응용 프로그램들은 (소켓 주소로 구분되는) 버스에 연결하여 같은 버스에 연결된 다른 응용 프로그램을 대상으로 메시지를 보내거나 모든 버스 구성원에게 브로드캐스트 신호를 보낼 수 있습니다. 버스에 연결된 응용 프로그램들에는 IP 주소와 유사한 버스 주소를 가지며, `org.freedesktop.Telepathy.AccountManager` 같은 DNS 이름처럼 몇 개의 잘 알려진 이름을 가질 수 있습니다. 모든 프로세스는, 메시지 전달과 이름 등록을 처리하는, D-Bus 데몬을 통해 통신합니다.

> 사용자의 관점에서 볼 때, 모든 시스템에는 두 개의 버스가 있습니다. 시스템 버스는 사용자가 시스템 전체에 걸쳐 있는 구성 요소(프린터, 블루투스, 하드웨어 관리 등)들과 통신하게 해 주며, 시스템을 사용하는 모든 사용자와 공유됩니다. 세션 버스는 사용자에게 고유한, 즉, 로그인된 사용자당 하나의 세션 버스가 있으며, 사용자의 응용 프로그램 간의 통신을 위해 사용됩니다. 응용 프로그램이 대량의 트래픽을 버스를 통해 전달해야 하는 경우, 사설 버스나, 중재자인 `dbus-daemon`이 없는 P2P 버스를 생성하여 통신할 수도 있습니다.

> libdus, GDBus, QtDBus, python-dbus 등 여러 라이브러리가 D-Bus 데몬과 통신하기 위한 D-Bus 프로토콜을 구현합니다. 이 라이브러리들은 D-Bus 메시지의 송수신, 언어의 타입을 D-Bus의 타입으로 마샬링, 그리고 객체를 버스에 발행하는 역할을 합니다. 이러한 라이브러리들은 주로, 연결됐거나 활성화 가능한 응용 프로그램들의 목록을 받아오거나, 버스에서 잘 알려진 이름들을 요청하는 편의성 API도 제공합니다. D-Bus 단에서 이 모든 것은 `dbus-daemon` 자체가 발행한 객체의 메서드를 호출하여 이루어집니다.

> D-Bus에 대한 더 자세한 정보는 [http://www.freedesktop.org/wiki/Software/dbus](http://www.freedesktop.org/wiki/Software/dbus) 에 있습니다.

## 20.1. Telepathy 프레임워크의 구성 요소

Telepathy는 모듈화되어 있으며, 각 모듈들은 D-Bus 메시징 버스를 통해 통신합니다. 대부분의 모듈은 사용자 세션 버스를 사용합니다. 이 통신은 Telepathy 명세에 상세히 명시되어 있습니다. 그림 20.1에 Telepathy 프레임워크의 구성 요소들이 나와 있습니다.

![Telepathy 구성 요소 예시](http://aosabook.org/images/telepathy/telepathy-components.png)

* Connection Manager는 Telepathy와 통신 서비스들간의 인터페이스를 제공합니다. XMPP, SIP, IRC 등을 위한 Connection Manager 등이 있습니다. 새로운 프로토콜에 대한 지원을 위해서는 해당 프로토콜을 위한 새로운 Connection Manager를 작성하면 됩니다.
* Account Manager 서비스는 사용자의 통신 계정들을 저장하고, 요청이 들어왔을 때 요청을 적합한 Connection Manager에 연결하는 역할을 합니다.
* Channel Dispatcher는 각 Connection Manager로부터 들어오는 채널을 듣고, 해당 종류의 채널(문자, 음성, 영상, 파일, 튜브 등)을 다룰 수 있다고 알린 클라이언트들에게 전달합니다. Channel Dispatcher는 특히 Telepathy 클라이언트가 아닌 응용 프로그램이 발송 채널을 요청하고 적절한 클라이언트가 그것을 지역적으로 처리할 수 있게 하는 서비스를 제공합니다. 이것은 응용 프로그램, 예를 들어 이메일 클라이언트가 연락처와의 텍스트 채팅을 요청하면, 인스턴스 메시징 클라이언트가 채팅 창을 보여주게 할 수 있습니다.
* Telepathy 클라이언트들은 들어오는 채널(문자, 음성, 영상, 파일, 튜브 등)에 대한 Connection Manager의 신호를 듣고, 해당 채널을 처리할 수 있는 클라이언트들에게 전달합니다. 클라이언트는 인스턴스 메신저, VoIP 클라이언트 등의 사용자 인터페이스와, 대화 로거 등의 서비스를 포함합니다. 클라이언트는 관심 있거나 처리하고자 하는 채널 종류의 목록과 함께 자신을 Channel Dispatcher에 등록합니다.

현재 버전의 Telepathy에서는, Account Manager와 Channel Dispatcher는 Mission Control이라는 하나의 프로세스가 제공하도록 구현되어 있습니다.

이러한 모듈화는 더그 맥일로이의 철학인 "단 한 가지 일만을 훌륭하게 처리하는 프로그램을 작성한다" 에 기반하였고, 몇 가지 중요한 이점을 가집니다:

* 견고함: 단일 요소의 결함은 전체 서비스를 무너지게 하지 않습니다.
* 개발의 편리함: 동작 중인 시스템의 구성 요소들은 다른 구성 요소에 영향을 주지 않으면서 교체될 수 있습니다. 개발 중인 모듈을 안정된 버전의 모듈과 비교하며 테스트할 수도 있습니다.
* 언어 독립성: 구성 요소들은 D-Bus 바인딩이 있는 어떠한 언어로도 작성될 수 있습니다. 주어진 커뮤니케이션 프로토콜의 가장 좋은 구현체가 특정 언어로 작성되었다면, 해당 언어로 Connection Manager를 작성할 수 있으며, 모든 Telepathy 클라이언트에서 사용될 수 있습니다. 비슷한 맥락에서, 어떤 언어로 사용자 인터페이스를 개발하든, 이용할 수 있는 프로토콜에 대한 제한이 없습니다.
* 라이센스 독립성: 시스템이 하나의 프로세스로 동작한다면 라이센스 호환이 안되겠지만, 서로 별개인 구성 요소로 이루어져 있기 때문에 구성 요소들은 서로 다른 소프트웨어 라이센스를 가질 수 있습니다.
* 인터페이스 독립성: 같은 Telepathy 구성 요소를 기반으로 다양한 사용자 인터페이스를 개발할 수 있습니다. 이것은 데스크톱 환경과 하드웨어 장치를 위한 네이티브 인터페이스 구현을 가능하게 합니다 (GNOME, KDE, Meego, Sugar 등).
* 보안: 구성 요소들은 각자의 주소공간에서 매우 제한된 권한을 가지고 실행됩니다. 예를 들어, 전형적인 Connection Manager는 네트워크와 D-Bus 세션 버스에 대한 접근 권한만을 필요로 하며, SELinux 같은 모듈을 사용하여 구성 요소의 자원 접근 권한을 제한할 수 있습니다.

Connection Manager는 여러 개의 Connection을 관리하며, 각 Connection은 통신 서비스와의 논리적인 연결을 나타냅니다. 설정된 계정 당 하나의 Connection이 존재하며, 하나의 Connection은 여러 개의 Channel을 포함합니다. Channel은 통신이 이루어지는 메커니즘입니다. Channel은 인스턴스 메신저 대화, 음성, 영상 통화, 파일 전송, 혹은 다른 상태를 유지해야 하는 작업일 수 있습니다. Connection과 Channel에 대해서는 20.3장에서 자세히 다뤄집니다.

## 20.2. How Telepathy uses D-Bus

## 20.2. Telepathy가 D-Bus를 사용하는 방식

Telepathy components communicate via a D-Bus messaging bus, which is usually the user's session bus. D-Bus provides features common to many IPC systems: each service publishes objects which have a strictly namespaced object path, like `/org/freedesktop/Telepathy/AccountManager3`. Each object implements a number of interfaces. Again strictly namespaced, these have forms like `org.freedesktop.DBus.Properties and ofdT.Connection`. Each interface provides methods, signals and properties that you can call, listen to, or request.

Telepathy 구성 요소들은 D-Bus 메시징 버스를 통해 통신하며, 주로 사용자의 세션 버스를 사용합니다. D-Bus는 많은 IPC 시스템에서 공통으로 찾아볼 수 있는 기능을 제공합니다. 서비스는 `/org/freedesktop/Telepathy/AccountManager3`처럼, 엄격히 정해진 이름공간의 객체 경로를 가진 객체를 발행하며, 각 객체는 몇 가지 인터페이스를 구현합니다. 이들 역시 `org.freedesktop.DBus.Properties and ofdT.Connection` 같은 형식의 엄격한 이름공간을 가지며, 인터페이스는 호출, 듣기, 또는 요청 가능한 메서드, 시그널, 그리고 속성을 제공합니다.

![D-Bus 서비스가 발행한 객체들의 개념적 표현](http://aosabook.org/images/telepathy/bus-hierarchy-conceptual.png)

> Publishing D-Bus Objects

> D-Bus 객체 발행하기

> Publishing D-Bus objects is handled entirely by the D-Bus library being used. In effect it is a mapping from a D-Bus object path to the software object implementing those interfaces. The paths of objects being published by a service are exposed by the optional `org.freedesktop.DBus.Introspectable` interface.

> D-Bus 객체 발행은 사용하는 온전히 D-Bus 라이브러리에 의해 처리됩니다. 결과적으로 볼 때, 객체 발행은 D-Bus 객체 경로를, 해당하는 인터페이스를 구현하는 소프트웨어 객체로 대응시키는 것입니다. 서비스가 발행하는 객체의 경로는 `org.freedesktop.DBus.Introspectable`이라는 선택적인 인터페이스에 의해 노출됩니다.

> When a service receives an incoming method call with a given destination path (e.g., `/ofdT/AccountManager`), the D-Bus library is responsible for locating the software object providing that D-Bus object and then making the appropriate method call on that object.

> 서비스가 `/ofdT/AccountManager`와 같이 지정된 목적지 경로를 가진 메서드 호출을 받으면, D-Bus 라이브러리는 해당하는 D-Bus 객체를 제공하는 소프트웨어 객체를 찾고, 찾은 객체에 대한 올바른 메서드 호출을 하는 역할을 합니다.

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

> You might wonder why each base class implements an `Interfaces` property, instead of relying on D-Bus' introspection capabilities to tell us what interfaces are available. The answer is that different channel and connection objects may offer different interfaces to each other, depending on the capabilities of the channel or connection, but that most of the implementations of D-Bus introspection assume that all objects of the same object class will have the same interfaces. For example, in `telepathy-glib`, the D-Bus interfaces listed by D-Bus introspection are retrieved from the object interfaces a class implements, which is statically defined at compile time. We work around this by having D-Bus introspection provide data for all the interfaces that could exist on an object, and use the `Interfaces` property to indicate which ones actually do.

> 왜 각 기반 클래스가, 사용 가능한 인터페이스들을 알려주는 D-Bus의 인트로스펙션 기능을 사용하지 않고 `Interfaces` 속성을 구현하는지 궁금하실 수도 있습니다. 그 이유는 서로 다른 채널과 커넥션 객체들은 가지는 기능에 따라 서로 다른 인터페이스를 가질 수 있지만, 대부분의 D-Bus 인트로스펙션 구현체들은 같은 객체 클래스의 모든 객체는 같은 인터페이스를 가진다고 가정하기 때문입니다. 예를 들어 `telepathy-glib`에선, D-Bus 인트로스펙션이 나열한 D-Bus 인터페이스들은 컴파일 타임에 정적으로 정의된 클래스가 구현하는 인터페이스들로부터 가져옵니다. 우리는 이 문제를 D-Bus 인트로스펙션에서 객체에 있을 수 있는 모든 인터페이스에 대한 정보를 제공하게 하고, `Interfaces` 속성이 실제로 객체가 가진 인터페이스를 정의하게 하여 회피합니다.

Although D-Bus itself provides no sanity checking that connection objects only have connection-related interfaces and so forth (since D-Bus has no concept of types, only arbitrarily named interfaces), we can use the information contained within the Telepathy specification to provide sanity checking within the Telepathy language bindings.

D-Bus 자체는 커넥션 객체가 커넥션과 관련된 인터페이스만 가지는지(D-Bus에는 임의의 기명 인터페이스만 있고 자료형에 대한 개념은 존재하지 않기 때문에) 따위에 대한 온전성을 확인해 주지 않지만, Telepathy 언어 바인딩 내 Telepathy 명세에 있는 정보를 사용하여 온전성 검사를 할 수 있습니다.

> Why and How the Specification IDL was Expanded

> IDL 명세가 왜, 어떻게 확장되었는가에 대해

> The existing D-Bus specification IDL defines the names, arguments, access restrictions and D-Bus type signatures of methods, properties and signals. It provides no support for documentation, binding hints or named types.

> 기존 D-Bus IDL 명세는 이름, 파라미터, 접근 제한, 메서드의 D-Bus 타입 시그니쳐, 속성, 그리고 시그널을 정의하지만, 문서, 바인딩 힌트, 기명 타입은 지원하지 않습니다.

> To resolve these limitations, a new XML namespace was added to provide the required information. This namespace was designed to be generic so that it could be used by other D-Bus APIs. New elements were added to include inline documentation, rationales, introduction and deprecation versions and potential exceptions from methods.

> 이러한 한계를 극복하기 위해, 필요한 정보를 제공하기 위한 새로운 XML 이름공간이 추가되었습니다. 이 이름공간은 제네릭 하게, 다른 D-Bus API들이 사용할 수 있도록 설계되었습니다. 인라인 문서, 근거, 서론, 대체된 버전들, 그리고 메서드에서 발생할 수 있는 예외를 포함하기 위한 엘리먼트들이 추가되었습니다.

> D-Bus type signatures are the low-level type notation of what is serialized over the bus. A D-Bus type signature may look like (ii) (which is a structure containing two int32s), or it may be more complex. For example, `a{sa(usuu)}`, is a map from string to an array of structures containing uint32, string, uint32, uint32 (Figure 20.3). These types, while descriptive of the data format, provide no semantic meaning to the information contained in the type.

> D-Bus 타입 시그니쳐는 버스 위에서 직렬화된 것들의 로우 레벨 타입 표기입니다. D-Bus 타입 시그니쳐는 `(ii)`(두개의 int32를 포함하는 구조체) 처럼 생겼거나, 더 복잡할 수도 있습니다. 예를 들어, `a{sa(usuu)}`는 uint32, string, uint32, uint32를 포함하는 구조체의 배열로 매핑된 string의 맵입니다(그림 20.3). 이 타입들은, 데이터 형식에 관해서 기술하지만, 타입에 저장된 정보에 대한 의미는 전혀 제공하지 않습니다.

> In an effort to provide semantic clarity for programmers and strengthen the typing for language bindings, new elements were added to name simple types, structs, maps, enums, and flags, providing their type signature, as well as documentation. Elements were also added in order to simulate object inheritance for D-Bus objects.

> 프로그래머들에게 의미론적 명료함을 제공하고 언어 바인딩을 위한 타이핑을 강화하기 위해 문서는 물론 간단한 타입, 구조체, 맵, 열거형, 플래그의 타입 시그니쳐를 제공하고, 들에 이름을 붙이기 위해, 새로운 엘리먼트들이 추가되었습니다.

![D-Bus 타입 (ii)와 a{sa(usuu)}](http://aosabook.org/images/telepathy/telepathy-types-unpacked.png)

### 20.2.1. Handles

### 20.2.1. 핸들

Handles are used in Telepathy to represent identifiers (e.g., contacts and room names). They are an unsigned integer value assigned by the connection manager, such that the tuple (connection, handle type, handle) uniquely refers to a given contact or room.

Telepathy에서는 식별자(e.g., 연락처와 대화방 이름)를 표현하기 위해 핸들을 사용합니다. 핸들은 Connection Manager에 의해 부호가 없는 정수 값이, 튜플(연결, 핸들 종류, 핸들)이 주어진 연락처나 대화방을 고유하게 참조할 수 있도록 할당됩니다.

Because different communications protocols normalize identifiers in different ways (e.g., case sensitivity, resources), handles provide a way for clients to determine if two identifiers are the same. They can request the handle for two different identifiers, and if the handle numbers match, then the identifiers refer to the same contact or room.

식별자를 표준화시는 방법이 통신 프로토콜마다 다르기 때문에(e.g., 대소문자 구분, 리소스), 핸들은 클라이언트에서 두 식별자가 같은지 확인할 수 있는 방법을 제공합니다. 클라이언트는 두 개의 서로 다른 식별자에 대한 핸들을 요청하고, 핸들 번호가 같은 경우 식별자가 같은 연락처나 대화방을 가리킨다는 것을 알 수 있습니다.

Identifier normalization rules are different for each protocol, so it is a mistake for clients to compare identifier strings to compare identifiers. For example, `escher@tuxedo.cat/bed` and `escher@tuxedo.cat/litterbox` are two instances of the same contact (`escher@tuxedo.cat`) in the XMPP protocol, and therefore have the same handle. It is possible for clients to request channels by either identifier or handle, but they should only ever use handles for comparison.

식별자의 표준화 규칙은 프로토콜마다 다르므로 식별자 문자열로 식별자를 구분하는 클라이언트는 잘못된 것입니다. 예를 들어, `escher@tuxedo.cat/bed`와 `escher@tuxedo.cat/litterbox`는 XMPP 프로토콜 내 같은 연락처(`escher@tuxedo.cat`)의 인스턴스이므로 같은 핸들을 가집니다. 클라이언트가 식별자나 핸들로 채널을 요청할 수는 있지만, 구분을 위해서는 핸들만을 사용해야 합니다.

### 20.2.2. Discovering Telepathy Services

### 20.2.2. Telepathy 서비스 발견

Some services, such as the Account Manager and the Channel Dispatcher, which always exist, have well known names that are defined in the Telepathy specification. However, the names of Connection Managers and clients are not well-known, and must be discovered.

Account Manager나 Channel Dispatcher같이 일부 상존하는 서비스들은 Telepathy 명세에 정의된 잘 알려진 이름을 가지고 있지만, Connection Manager들의 이름은 잘 알려지지 않았으며, 발견되어야 합니다.

There's no service in Telepathy responsible for the registration of running Connection Managers and Clients. Instead, interested parties listen on the D-Bus for the announcement of a new service. The D-Bus bus daemon will emit a signal whenever a new named D-Bus service appears on the bus. The names of Clients and Connection Managers begin with known prefixes, defined by the specification, and new names can be matched against these.

Telepathy에는 실행 중인 Connection Manager와 Client의 등록 관리를 하는 서비스가 없습니다. 대신, D-Bus 데몬은 새로운 D-Bus 서비스가 버스에 나타났을 때 신호를 발신하므로, 이해관계자들이 D-Bus 위에서 새로운 서비스의 선언을 들을 수 있습니다. 클라이언트와 Connection Manager들의 이름은 명세에 정의된, 알려진 접두어로 시작하며, 새로운 이름들은 이들과 비교할 수 있습니다.

The advantage of this design is that it's completely stateless. When a Telepathy component is starting up, it can ask the bus daemon (which has a canonical list, based on its open connections) what services are currently running. For instance, if the Account Manager crashes, it can look to see what connections are running, and reassociate those with its account objects.

이러한 디자인은, 상태를 가지지 않는다는 장점을 가집니다. Telepathy 구성 요소가 시작할 때, 버스 데몬(열려 있는 연결들을 기반으로, 규범적인 목록을 가지고 있음)에 어떤 서비스들이 실행 중인지 물어볼 수 있습니다. 예를 들어, Account Manager가 비정상적으로 종료되어도 실행 중인 연결들을 확인하여 다시 계정 객체들과 연관시킬 수 있습니다.

> Connections are Services Too

> Connection도 서비스다

> As well as the Connection Managers themselves, the connections are also advertised as D-Bus services. This hypothetically allows for the Connection Manager to fork each connection off as a separate process, but to date no Connection Manager like this has been implemented. More practically, it allows all running connections to be discovered by querying the D-Bus bus daemon for all services beginning with `ofdT.Connection`.

> Connection Manager는 물론, Connection 자체도 D-Bus 서비스로 선언됩니다. 이것은 이론적으로 Connection Manager가 각 연결을 개별 프로세스로 포크 할 수 있게 해주지만, 아직 그런 Connection Manager는 존재하지 않습니다. 좀 더 실용적인 면에선, 모든 D-Bus 데몬에 요청을 보냄으로써 이름이 `ofdT.Connection`으로 시작하는 실행 중인 모든 연결들을 발견할 수 있게 해줍니다.

> The Channel Dispatcher also uses this method to discover Telepathy clients. These begin with the name ofdT.Client, e.g., ofdT.Client.Logger.

> Channel Dispatcher 역시 Telepathy 클라이언트들을 발견하기 위해 이 방법을 사용합니다. 이러한 클라이언트들은 `ofdT.Client.Logger` 처럼 `ofdT.Client`로 시작합니다.

### 20.2.3. Reducing D-Bus Traffic

### 20.2.3. D-Bus 트래픽 줄이기

Original versions of the Telepathy specification created an excessive amount of D-Bus traffic in the form of method calls requesting information desired by lots of consumers on the bus. Later versions of the Telepathy have addressed this through a number of optimizations.

초기 Telepathy 명세는 버스 위의 많은 소비자들이 원하는, 정보를 요청하기 위한 메서드 콜의 형태로 과다한 D-Bus 트래픽을 발생시켰습니다. 이후 버전의 Telepathy에서는 몇 가지 최적화를 통해 이 문제를 해결하였습니다.

Individual method calls were replaced by D-Bus properties. The original specification included separate method calls for object properties: `GetInterfaces`, `GetChannelType`, etc. Requesting all the properties of an object required several method calls, each with its own calling overhead. By using D-Bus properties, everything can be requested at once using the standard `GetAll` method.

개별 메서드 호출이 D-Bus 속성으로 대체되었습니다. 기존 명세에선 `GetInterfaces`, `GetChannelType` 등 객체 속성에 대응하는 메서드 호출을 따로 두었으며, 각각의 호출 오버헤드를 가집니다. 이후 이를 D-Bus 속성으로 대체함으로써 표준 `GetAll` 메서드로 모든 속성을 한번에 가져올 수 있게 되었습니다.

Furthermore, quite a number of properties on a channel are immutable for the lifetime of the channel. These include things like the channel's type, interfaces, who it's connected to and the requestor. For a file transfer channel, for example, it also includes things like the file size and its content type.

게다가 채널 타입, 인터페이스, 연결되어 있는 대상, 요청자 등 많은 수의 채널 속성은 채널이 살아 있는 동안 바뀌지 않습니다. 이러한 불변의 속성의 예로 파일 전송 채널을 들면, 파일 크기와 컨텐츠 타입이 있습니다.

A new signal was added to herald the creation of channels (both incoming and in response to outgoing requests) that includes a hash table of the immutable properties. This can be passed directly to the channel proxy constructor (see Section 20.4), which saves interested clients from having to request this information individually.

불변 속성에 대한 해쉬 테이블을 포함하는, 채널의 생성을 알리기 위한 새로운 신호가 추가되었습니다. 이 신호는 클라이언트가 각자 정보를 요청할 필요 없이 채널 생성자 프록시에 직접 전달될 수 있습니다(20.4장 참고).

User avatars are transmitted across the bus as byte arrays. Although Telepathy already used tokens to refer to avatars, allowing clients to know when they needed a new avatar and to save downloading unrequired avatars, each client had to individually request the avatar via a `RequestAvatar` method that returned the avatar as its reply. Thus, when the Connection Manager signalled that a contact had updated its avatar, several individual requests for the avatar would be made, requiring the avatar to be transmitted over the message bus several times.

사용자의 아바타는 바이트 배열의 형태로 버스를 통해 전송되었습니다. 이미 Telepathy에서는 클라이언트들에게 새로운 아바타가 필요함을 알리고, 불필요한 아바타를 받는 비용을 줄일 수 있도록 아바타를 토큰으로 구분하고 있었지만, 클라이언트들은 `RequestAvatar` 메서드를 통해 아바타를 하나하나 가져와야 했습니다. 따라서, Connetion Manager가 어떤 연락처가 아바타를 갱신하였다는 신호를 보내면, 아바타를 요청하는 다수의 개별 요청이 일어났었고, 같은 아바타가 버스를 통해 여러 번 전송되야 했습니다.

This was resolved by adding a new method which did not return the avatar (it returns nothing). Instead, it placed the avatar in a request queue. Retrieving the avatar from the network would result in a signal, `AvatarRetrieved`, that all interested clients could listen to. This means the avatar data only needs to be transmitted over the bus once, and will be available to all the interested clients. Once the client's request was in the queue, all further client requests can be ignored until the emission of the AvatarRetrieved.

이 문제는 아바타를 반환하지 않는(아무 것도 반환하지 않는) 새로운 메서드를 추가함으로써 해결되었습니다. 대신 이 메서드는, 아바타를 요청 큐에 넣습니다. 네트워크로부터 아바타를 가져오면 `AvatarRetrieved` 신호가 보내지게 되며, 이에 대해 관심이 있는 모든 클라이언트가 이용 가능합니다. 클라이언트의 요청이 큐에 들어간 이상, `AvatarRetrieved` 신호의 송출 이전의 클라이언트 요청은 무시 가능합니다.

Whenever a large number of contacts need to be loaded (i.e., when loading the contact roster), a significant amount of information needs to be requested: their aliases, avatars, capabilities, and group memberships, and possibly their location, address, and telephone numbers. Previously in Telepathy this would require one method call per information group (most API calls, such as GetAliases already took a list of contacts), resulting in half a dozen or more method calls.

많은 수의 연락처를 불러와야 할 때 마다(i.e., 연락처 목록을 불러올 때), 별명, 아바타, 기능, 구성하는 그룹을 포함하고, 위치, 주소, 전화번호 등을 포함할 수도 있는 상당한 양의 정보가 요청되어야 합니다. 이전 Telepathy 버전에서는 하나의 정보 그룹 마다 하나의 메서드 호출(`GetAliases` 등 대부분의 API 호출들은 이미 연락처 목록을 요구했습니다)을 해야 했고, 이 작업은 여섯 개 이상의 메서드 호출을 초래했습니다.

To solve this, the Contacts interface was introduced. It allowed information from multiple interfaces to be returned via a single method call. The Telepathy specification was expanded to include Contact Attributes: namespaced properties returned by the GetContactAttributes method that shadowed method calls used to retrieve contact information. A client calls `GetContactAttributes` with a list of contacts and interfaces it is interested in, and gets back a map from contacts to a map of contact attributes to values.

이 문제를 해결해기 위해 Contacts 인터페이스가 도입되어, 여러 인터페이스로부터의 정보를 한 번의 메서드 호출로 가져올 수 있게 되었습니다. Telepathy 명세는 `GetContactAttribute` 메서드가 반환하는 이름공간을 가진 속성이, Contact 속성을 포함하도록 확장되었으며, 이로 인해 연락처 정보를 가져오기 위해 사용되었던 메서드 콜은 더 이상 사용되지 않게 되었습니다. 클라이언트가 `GetContactAttributes` 메서드를 연락처의 목록과, 관심이 있는 인터페이스와 함께 호출하면 연락처의 매핑으로부터 연락처 속성과 그에 대한 값과 대응되는 매핑을 돌려받게 됩니다.

A bit of code will make this clearer. The request looks like this:

코드를 보면 좀 더 명확해집니다. 요청을 다음과 같이 생겼습니다:

	connection[CONNECTION_INTERFACE_CONTACTS].GetContactAttributes(
	  [ 1, 2, 3 ], # contact handles
	  [ "ofdT.Connection.Interface.Aliasing",
	    "ofdT.Connection.Interface.Avatars",
	    "ofdT.Connection.Interface.ContactGroups",
	    "ofdT.Connection.Interface.Location"
	  ],
	  False # 이 연락처들에 대한 레퍼런스를 가지고 있지 말라
	)

and the reply might look like this:

응답은 이렇게 생길 수 있습니다:

	{ 1: { 'ofdT.Connection.Interface.Aliasing/alias': 'Harvey Cat',
	       'ofdT.Connection.Interface.Avatars/token': hex string,
	       'ofdT.Connection.Interface.Location/location': location,
	       'ofdT.Connection.Interface.ContactGroups/groups': [ 'Squid House' ],
	       'ofdT.Connection/contact-id': 'harvey@nom.cat'
	     },
	  2: { 'ofdT.Connection.Interface.Aliasing/alias': 'Escher Cat',
	       'ofdT.Connection.Interface.Avatars/token': hex string,
	       'ofdT.Connection.Interface.Location/location': location,
	       'ofdT.Connection.Interface.ContactGroups/groups': [],
	       'ofdT.Connection/contact-id': 'escher@tuxedo.cat'
	     },
	  3: { 'ofdT.Connection.Interface.Aliasing/alias': 'Cami Cat',
	        ⋮    ⋮    ⋮
	     }
}

## 20.3. Connections, Channels and Clients

## 20.3. Connection, Channel, 그리고 Client

### 20.3.1. Connections

### 20.3.1. Connection

A Connection is created by the Connection Manager to establish a connection to a single protocol/account. For example, connecting to the XMPP accounts `escher@tuxedo.cat` and `cami@egg.cat` would result in two Connections, each represented by a D-Bus object. Connections are typically set up by the Account Manager, for the currently enabled accounts.

Connection은 하나의 계정 당 하나의 프로토콜을 연결하기 위해 Connection Manager에 의해 만들어집니다. 예를 들어, XMPP 계정인 `escher@tuxedo.cat`과 `cami@egg.cat`에 연결하는 것은 D-Bus 객체로 표현된 두 개의 Connection을 만들게 됩니다. Connection은 주로 현재 활성화된 계정에 대해, Account Manager에 의해 구성됩니다.

The Connection provides some mandatory functionality for managing and monitoring the connection status and for requesting channels. It can then also provide a number of optional features, depending on the features of the protocol. These are provided as optional D-Bus interfaces (as discussed in the previous section) and listed by the Connection's `Interfaces` property.

Connection은 연결 상태를 관찰, 관리하고, 채널을 요청하기 위한 몇 가지 필수적인 기능을 제공하며, 프로토콜의 기능에 따라 몇가지 선택적인 기능을 제공하기도 합니다. 이러한 기능들은 선택적인 (이전 장에서 다뤄졌던 것 처럼) D-Bus 인터페이스로 제공되며, Connection의 `Interfaces` 속성에 의해 나열됩니다.

Typically Connections are managed by the Account Manager, created using the properties of the respective accounts. The Account Manager will also synchronize the user's presence for each account to its respective connection and can be asked to provide the connection path for a given account.

Connection들은 주로 Account Manager에 의해 관리되며, 해당하는 계정의 속성을 사용하여 만들어집니다. Account Manager는 각 계정에 대한 사용자의 부재 여부를 각 연결에 동기화시키고, 주어진 계정에 대한 연결 경로를 제공하기도 합니다.

### 20.3.2. Channels

### 20.3.2. 채널

Channels are the mechanism through which communications are carried out. A channel is typically an IM conversation, voice or video call or file transfer, but channels are also used to provide some stateful communication with the server itself, (e.g., to search for chat rooms or contacts). Each channel is represented by a D-Bus object.

채널은 통신이 이루어지는 메커니즘입니다. 채널은 주로 인스턴트 메신저 대화, 음성, 영상 통화나 파일 전송이지만, 서버 자체와의 상태 유지 통신(e.g., 대화방이나 연락처 검색)을 제공할 수도 있습니다. 각 채널은 D-Bus 객체로 나타내어집니다.

Channels are typically between two or more users, one of whom is yourself. They typically have a target identifier, which is either another contact, in the case of one-to-one communication; or a room identifier, in the case of multi-user communication (e.g., a chat room). Multi-user channels expose the `Group` interface, which lets you track the contacts who are currently in the channel.

체널은 주로 둘 이상의 사용자들간에 이루어지며, 그 중 하나는 자신입니다. 채널은 주로 타겟 식별자를 가지고 있으며, 이는 주로 1:1 통신일 경우엔 다른 연락처이거나, 다중 사용자 통신일 경우(e.g., 대화방)엔 방 식별자입니다. 다중 사용자 채널은 `Group` 인터페이스를 노출하며, 이를 통해 현재 채널에 있는 연락처들을 추적할 수 있습니다.

Channels belong to a Connection, and are requested from the Connection Manager, usually via the Channel Dispatcher; or they are created by the Connection in response to a network event (e.g., incoming chat), and handed to the Channel Dispatcher for dispatching.

채널은 Connection에 속하며, 주로 Channel Dispatcher를 통해 Connection Manager로부터 요청이 들어오거나, 네트워크 이벤트(e.g., 걸려오는 대화)의 응답으로써 Connection에 의해 만들어지며, 이후 연결을 위해 Channel Dispatcher로 넘어갑니다.

The type of channel is defined by the channel's ChannelType property. The core features, methods, properties, and signals that are needed for this channel type (e.g., sending and receiving text messages) are defined in the appropriate `Channel.Type` D-Bus interface, for instance `Channel.Type.Text`. Some channel types may implement optional additional features (e.g., encryption) which appear as additional interfaces listed by the channel's `Interfaces` property. An example text channel that connects the user to a multi-user chatroom might have the interfaces shown in Table 20.1.

채널의 타입은 채널의 `ChannelType` 속성에 정의되어 있습니다. 해당 채널 타입(e.g., 문자 메시지를 송수신함)에 필요한 핵심 기능, 메서드, 속성, 신호들은 `Channel.Type.Text` 처럼 적절한 `Channel.Type` D-Bus 인터페이스에 정의되어 있습니다. 어떤 채널 타입들은 선택적인 추가 기능(e.g., 암호화)을 구현할 수 있으며, 채널의 `Interfaces` 속성에 추가적 인터페이스로 나열되어 있습니다. 표 20.1에는 다중 사용자 대화방에 연결하는 텍스트 채널의 한 예가 가질 수 있는 인터페이스를 보여줍니다.

속성 | 목적
- | -
`odfT.Channel` | 모든 채널에 공통적인 기능
`odfT.Channel.Type.Text` | 채널 타입(텍스트 채널에 공통적인 기능들을 포함)
`odfT.Channel.Interface.Messages` | 서식 있는 텍스트 메시징
`odfT.Channel.Interface.Group` | 이 채널의 구성원을 나열, 추적, 초대, 승인
`odfT.Channel.Interface.Room` | 제목 등 대화방의 속성을 읽고 쓰기

표 20.1: 예시 텍스트 채널

> Contact List Channels: A Mistake

> 연락처 목록 채널: 실수

> In the first versions of the Telepathy specification, contact lists were considered a type of channel. There were several server-defined contact lists (subscribed users, publish-to users, blocked users), that could be requested from each Connection. The members of the list were then discovered using the Group interface, like for a multi-user chat.

> 초기 Telepathy 명세에선 연락처 목록을 채널의 일종으로 정의합니다. 각 Connection에서 요청할 수 있는, 서버에서 지정하는 여러 연락처 목록(구독한 사용자, 발행 대상 사용자, 차단된 사용자)이 있었으며, 목록의 구성원들은 다중 사용자 채팅과 같이 Group 인터페이스를 통해 발견되었습니다.

> Originally this would allow for channel creation to occur only once the contact list had been retrieved, which takes time on some protocols. A client could request the channel whenever it liked, and it would be delivered once ready, but for users with lots of contacts this meant the request would occasionally time out. Determining the subscription/publish/blocked status of a client required checking three channels.

> 기존에 방식에서의 채널 생성은, 일부 프로토콜에서는 어느 정도의 시간이 걸리는, 연락처 목록을 가져 온 다음에 한 번만 채널이 생성되었습니다. 클라이언트는 채널을 원할 때 요청하고 준비가 되면 받을 수 있지만, 연락처가 많은 사용자들에겐 이 요청은 종종 타임아웃이 나게 됩니다. 클라이언트의 구독/발행/차단 상태를 결정짓기 위해서는 세 가지 채널을 확인해야 했습니다.

> Contact Groups (e.g., Friends) were also exposed as channels, one channel per group. This proved extremely difficult for client developers to work with. Operations like getting the list of groups a contact was in required a significant amount of code in the client. Further, with the information only available via channels, properties such as a contact's groups or subscription state could not be published via the Contacts interface.

> 연락처 그룹(e.g., 친구들) 역시 그룹 당 하나의 채널의 형태로 노출되어 있었습니다. 이러한 구조는 클라이언트 개발자들이 다루기 매우 힘든 것으로 증명되었습니다. 연락처가 속해 있는 그룹의 목록을 가져오는 등의 작업은 클라이언트 측에서 매우 많은 양의 코드를 필요로 했습니다. 또, 채널을 통해서만 정보를 받아올 수 있기 때문에, 연락처의 그룹이나 구독 상태를 Contacts 인터페이스를 통해 발행할 수 없었습니다. 

> Both channel types have since been replaced by interfaces on the Connection itself which expose contact roster information in ways more useful to client authors, including subscription state of a contact (an enum), groups a contact is in, and contacts in a group. A signal indicates when the contact list has been prepared.

> 두 채널 타입 모두 클라이언트 개발자에게 유용한 연락처 목록 정보를 노출하는, 연락처의 구독 상태(enum 형의), 연락처가 속해 있는 그룹, 그리고 그룹에 있는 연락처들을 포함하는 Connection 자체의 인터페이스로 교체되었습니다. 시그널은 연락처 목록이 준비되었는지 여부를 알려줍니다.

### 20.3.3. Requesting Channels, Channel Properties and Dispatching

Channels are requested using a map of properties you wish the desired channel to possess. Typically, the channel request will include the channel type, target handle type (contact or room) and target. However, a channel request may also include properties such as the filename and filesize for file transfers, whether to initially include audio and video for calls, what existing channels to combine into a conference call, or which contact server to conduct a contact search on.

채널은 채널이 가지길 원하는 속성들의 매핑을 사용해서 요청할 수 있습니다. 일반적으로 채널 요청은 채널 타입, 타겟 핸들 타입(연락처 또는 대화방)과 타겟을 포함합니다. 하지만, 채널 요청은 파일 전송에 대해서 파일 이름이나 파일 크기, 전화 요청에 초기 음성이나 영상, 전화 회의에 합칠 기존의 채널, 연락처 검색에 사용할 연락처 서버 등을 포함할 수도 있습니다.

The properties in the channel request are properties defined by interfaces of the Telepathy spec, such as the ChannelType property (Table 20.2). They are qualified with the namespace of the interface they come from. Properties which can be included in channel requests are marked as requestable in the Telepathy spec.

채널 요청의 속성들은 ChannelType 속성(표 20.2) 등 Telepathy 인터페이스 명세에 정의되어 있는 속성들입니다. 이 속성들은 인터페이스의 이름공간에 의해 자격을 갖춥니다. 채널 요청에 포함될 수 있는 속성들은 요청될 수 있다고 Telepathy 명세에 정의되어 있습니다.

Property | Value
- | -
`ofdT.Channel.ChannelType` | `ofdT.Channel.Type.Text`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact` (1)
`ofdT.Channel.TargetID` | `escher@tuxedo.cat`

표 20.2: 채널 요청의 예시

The more complicated example in Table 20.3 requests a file transfer channel. Notice how the requested properties are qualified by the interface from which they come. (For brevity, not all required properties are shown.)

표 20.3의 좀 더 복잡한, 파일 전송 채널을 요청하는 예시가 있습니다. 요청된 속성들이 소속된 인터페이스에 대해 적합함을 확인할 수 있습니다. (간략함을 위해 필요한 속성들의 일부만 표시하였습니다).

Property | Value
- | -
ofdT.Channel.ChannelType | ofdT.Channel.Type.FileTransfer
ofdT.Channel.TargetHandleType | Handle_Type_Contact (1)
ofdT.Channel.TargetID | escher@tuxedo.cat
ofdT.Channel.Type.FileTransfer.Filename | meow.jpg
ofdT.Channel.Type.FileTransfer.ContentType | image/jpeg

표 20.3: 파일 전송 채널 요청

Channels can either be created or ensured. Ensuring a channel means creating it only if it does not already exist. Asking to create a channel will either result in a completely new and separate channel being created, or in an error being generated if multiple copies of such a channel cannot exist. Typically you wish to ensure text channels and calls (i.e., you only need one conversation open with a person, and in fact many protocols do not support multiple separate conversations with the same contact), and wish to create file transfers and stateful channels.

채널들은 생성되거나 확보될 수 있습니다. 채널을 확보한다는 것은 채널이 존재하지 않을 시에만 생성한다는 뜻입니다. 채널 생성을 요청하는 것은 완전히 새롭고 별개의 채널이 생기거나, 해당 채널의 사본이 존재할 수 없을 시엔 오류가 납니다. 보통 텍스트 채널과 통화를 확보하며(i.e., 보통 한 사람에 대해 하나의 대화만 원할 뿐더러, 많은 프로토콜들은 같은 연락처와의 여러 개의 대화를 지원하지 않습니다), 파일 전송과, 상태가 있는 채널을 생성하길 원합니다.

Newly created channels (requested or otherwise) are announced by a signal from the Connection. This signal includes a map of the channel's immutable properties. These are the properties which are guaranteed not to change throughout the channel's lifetime. Properties which are considered immutable are marked as such in the Telepathy spec, but typically include the channel's type, target handle type, target, initiator (who created the channel) and interfaces. Properties such as the channel's state are obviously not included.

새롭게 생성된 채널들은(요청되었거나 아니거나) Connection에서 시그널에 의해 선언됩니다. 이 시그널은 채널의 불변 속성들의 매핑을 포함합니다. 이 속성들은 채널이 존재하는 동안 변하지 않음이 보장되어 있습니다. 변하지 않을 것이라고 간주되는 속성들은 Telepathy의 명세에 표시되어 있으나, 보통 채널의 타입, 타켓 핸들 타입, 타겟, 창시자(채널을 만든 사람), 그리고 인터페이스들을 포함합니다. 물론 채널의 상태 같은 속성들은 포함되지 않습니다.

> Old-School Channel Requesting

> 옛날 방식의 채널 요청

> Channels were originally requested simply by type, handle type and target handle. This wasn't sufficiently flexible because not all channels have a target (e.g., contact search channels), and some channels require additional information included in the initial channel request (e.g., file transfers, requesting voicemails and channels for sending SMSes).

> 기존에는, 채널들은 타입, 핸들 타입, 그리고 타겟 핸들으로 요청되었습니다. 이것은 모든 채널들이 타겟을 가지기 않고(e.g., 연락처 검색 채널), 일부 채널들은 초기 채널 요청에 추가적인 정보를 포함해야 했기 때문에(e.g., 파일 전송, 음성 메시지 요청, SMS 전송 채널 등) 충분히 유연하지 않았습니다.

> It was also discovered that two different behaviors might be desired when a channel was requested (either to create a guaranteed unique channel, or simply ensure a channel existed), and until this time the Connection had been responsible for deciding which behavior would occur. Hence, the old method was replaced by the newer, more flexible, more explicit ones.

> 또, 채널을 요청할 때 두 개의 서로 다른 동작이 일어날 수 있음이 발견되었으며(고유함이 보장된 채널을 생성하거나, 단순히 채널이 존재하는지 확인하거나), 이 전까지는 Connection이 어떤 동작이 일어날지 정해야 했습니다. 따라서, 기존의 방식은 새롭고, 더 유연하고, 더 명시적인 방식으로 교체되었습니다.

Returning a channel's immutable properties when you create or ensure the channel makes it much faster to create a proxy object for the channel. This is information we now don't have to request. The map in Table 20.4 shows the immutable properties that might be included when we request a text channel (i.e., using the channel request in Table 20.3). Some properties (including TargetHandle and InitiatorHandle) have been excluded for brevity.

채널을 확보하거나 생성할 때 채널의 불변 속성들은 반환하는 것은 채널에 대한 프록시 객체를 만드는 것을 훨씬 빠르게 합니다. 이 정보은 이제 확보하기 위해 요청을 보낼 필요가 없습니다. 표 20.4의 매핑은 텍스트 채널을 요청할 때(즉, 표 20.3의 채널 요청을 사용하여) 포함될 수 있는 불변 속성들을 보여줍니다. 일부 속성들은(TargetHandle과 InitiatorHandle 등)은 간결함을 위해 생략되었습니다.

Property | Value
- | -
`ofdT.Channel.ChannelType` | `Channel.Type.Text`
`ofdT.Channel.Interfaces` | `{[} Channel.Interface.Messages`, `Channel.Interface.Destroyable`, `Channel.Interface.ChatState {]}`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact` (1)
`ofdT.Channel.TargetID` | `escher@tuxedo.cat`
`ofdT.Channel.InitiatorID` | `danielle.madeley@collabora.co.uk`
`ofdT.Channel.Requested` | `True`
`ofdT.Channel.Interface.Messages.SupportedContentTypes` | `{[} text/html, text/plain {]}`

Table 20.4: Example Immutable Properties Returned by a New Channel

표 20.4: 새로운 채널에 의해 반환된 불변 속성들의 예시

The requesting program typically makes a request for a channel to the Channel Dispatcher, providing the account the request is for, the channel request, and optionally the name of a the desired handler (useful if the program wishes to handle the channel itself). Passing the name of an account instead of a connection means that the Channel Dispatcher can ask the Account Manager to bring an account online if required.

요청하는 프로그램은 주로 Channel Dispatcher에 요청을 위한 계정, 채널 요청, 그리고 선택적으로 원하는 핸들러 이름(프로그램이 채널을 직접 다룰 경우 유용합니다)을 포함하여 채널 요청을 보냅니다. 계정의 연결 대신 이름을 넘겨주는 것은 Channel Dispatcher가 필요할 경우 Account Manager에 계정을 온라인 상태로 전환시킬 것을 요청할 수 있게 합니다.

Once the request is complete, the Channel Dispatcher will either pass the channel to the named Handler, or locate an appropriate Handler (see below for discussion on Handlers and other clients). Making the name of the desired Handler optional makes it possible for programs that have no interest in communication channels beyond the initial request to request channels and have them handled by the best program available (e.g., launching a text chat from your email client).

요청이 완료되면, Channel Dispatcher는 채널을 기명 Handler에 전달하거나 적절한 Handler(Handler와 다른 클라이언트에 대한 논의는 아래에 있습니다)를 찾습니다. 원하는 Handler의 이름을 선택 사항으로 만든 것은 초기 요청 이후 채널과의 통신이 필요 없는 프로그램들이 채널을 요청한 후 다른 프로그램이 처리할 수 있게(e.g., 이메일 클라이언트에서 텍스트 채팅을 시작하는 등) 하기 위함입니다.

![http://aosabook.org/images/telepathy/dispatching-model.png](Channel Request and Dispatching)
![http://aosabook.org/images/telepathy/dispatching-model.png](Channel Request and Dispatching)

그림 20.4: 채널 요청과 배포

The requesting program makes a channel request to the Channel Dispatcher, which in turn forwards the request to the appropriate Connection. The Connection emits the NewChannels signal which is picked up by the Channel Dispatcher, which then finds the appropriate client to handle the channel. Incoming, unrequested channels are dispatched in much the same way, with a signal from the Connection that is picked up by the Channel Dispatcher, but obviously without the initial request from a program.

요청하는 프로그램은 Channel Dispathcer에 채널 요청을 보내고, 그것은 또다시 적절한 Connection에 요청을 전달합니다. Connection은 NewChannels 시그널을 발신하고, 이 시그널은 Channel Dispatcher에 의해 수집되며 해당 채널을 처리할 수 있는 적절한 클라이언트를 찾습니다. 들어오는, 요청받지 않은 채널들은 비슷한 방식으로 배포됩니다. Connection으로부터의 시그널은 Connection Dispatcher에 의해 수집되지만, 초기에 프로그램으로부터의 요청은 존재하지 않습니다.

### 20.3.4. Clients

### 20.3.4. 클라이언트

Clients handle or observe incoming and outgoing communications channels. A client is anything that is registered with the Channel Dispatcher. There are three types of clients (though a single client may be two, or all three, types if the developer wishes):

클라이언트들은 수신 및 발신 채널들을 처리하거나 관찰합니다. 클라이언트는 Channel Dispatcher에 등록 된 어떤 것이 될수도 있습니다. Telepathy에는 세 종류의 클라이언트가 있습니다(개발자가 원할 경우 하나의 클라이언트는 이 종류들 중에 두 개, 혹은 세 개 모두의 종류가 될 수 있습니다):

* Observers: Observe channels without interacting with them. Observers tend to be used for chat and activity logging (e.g., incoming and outgoing VoIP calls).
* Approvers: Responsible for giving users an opportunity to accept or reject an incoming channel.
* Handlers: Actually interact with the channel. That might be acknowledging and sending text messages, sending or receiving a file, etc. A Handler tends to be associated with a user interface.

* Observer: 채널에 개입하지 않고 관찰합니다. Observer들은 채팅과 활동 기록(수신 및 발신 VoIP 통화 등)에 주로 쓰입니다.
* Approver: 사용자들이 수신 채널을 허용하거나 차단할 수 있는 기회를 줍니다.
* Handler: 문자 메시지들을 승인하거나 보내기, 파일을 보내거나 받기 등 채널과 실제로 상호 작용을 합니다. Handler는 사용자 인터페이스와 주로 연관됩니다.

Clients offer D-Bus services with up to three interfaces: Client.Observer, Client.Approver, and Client.Handler. Each interface provides a method that the Channel Dispatcher can call to inform the client about a channel to observe, approve or handle.

클라이언트들은 Client.Observer, Client.Approver, 그리고 Client 총 세 개의 인터페이스들에게 D-Bus 서비스를 제공할 수 있습니다. 각 인터페이스는 Channel Dispatcher가 클라이언트에게 관찰, 승인, 혹은 처리할 채널에 대해 알려 주기 위해 호출할 수 있는 메서드를 제공합니다. 

The Channel Dispatcher dispatches the channel to each group of clients in turn. First, the channel is dispatched to all appropriate Observers. Once they have all returned, the channel is dispatched to all the appropriate Approvers. Once the first Approver has approved or rejected the channel, all other Approvers are informed and the channel is finally dispatched to the Handler. Channel dispatching is done in stages because Observers might need time to get set up before the Handler begins altering the channel.

Channel Dispatcher는 클라이언트들의 그룹에 채널을 순차적으로 배포합니다. 먼저, 채널을 모든 적절한 Observer들에게 배포합니다. 모두 반환된 이후, 채널은 모든 적절한 Approver들에게 배포됩니다. 첫번째 Approver가 채널을 허용하거나 차단했을 때, 모든 Approver들에게 채널이 Handler에 최종적으로 배포되었다는 정보가 전달됩니다. 채널 배포는 Observer들이 Handler가 채널을 변경시키기 전에, 구성하는 데 시간이 필요할 수 있기 때문에 단계별로 실행됩니다.

Clients expose a channel filter property which is a list of filters read by the Channel Dispatcher so that it knows what sorts of channels a client is interested in. A filter must include at least the channel type, and target handle type (e.g., contact or room) that the client is interested in, but it can contain more properties. Matching is done against the channel's immutable properties, using simple equality for comparison. The filter in Table 20.5 matches all one-to-one text channels.

클라이언트들은 Channel Dispatcher가 읽어들여 클라이언트가 관심 있어하는 채널들의 종류를 알 수 있게 하는 채널 필터의 목록인 채널 필터 속성을 드러냅니다. 필터는 최소한 클라이언트가 관심 있어 하는 채널 타입과 타겟 핸들 타입(연락처 또는 대화방)을 포함해야 하며, 더 많은 속성들을 포함할 수도 있습니다. 매칭은 채널의 불변 속성에 대해 단순히 동등성을 비교하여 이루어집니다. 표 20.5의 필터는 모든 1:1 텍스트 채널에 매칭됩니다.

Property | Value
- | -
`ofdT.Channel.ChannelType` | `Channel.Type.Text`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact` (1)

Table 20.5: Example Channel Filter

표 20.5: 채널 필터의 예시

Clients are discoverable via D-Bus because they publish services beginning with the well-known name `ofdT.Client` (for example `ofdT.Client.Empathy.Chat`). They can also optionally install a file which the Channel Dispatcher will read specifying the channel filters. This allows the Channel Dispatcher to start a client if it is not already running. Having clients be discoverable in this way makes the choice of user interface configurable and changeable at any time without having to replace any other part of Telepathy.

클라이언트들은 잘 알려진 이름 `ofdT.Client`으로 시작하는 서비스들(예를 들어, `ofdT.Client.Empathy.Chat`)을 발행하기 때문에 D-Bus를 통해 발견될 수 있습니다. 또, Channel Dispatcher가 읽고 채널 필터를 정의할 수 있도록 선택적으로 파일을 설치할 수도 있습니다. 이것은 Channel Dispather가 클라이언트가 실행되고 있지 않을 경우에 클라이언트를 실행할 수 있도록 합니다. 이러한 방식으로 클라이언트를 발견 가능할 수 있게 하는 것은 Telepathy의 다른 부분을 교체하지 않고도 사용자 인터페이스를 어느 때라도 설정, 수정 가능할 수 있게 합니다.

> All or Nothing

> 모 아니면 도

> It is possible to provide a filter indicating you are interested in all channels, but in practice this is only useful as an example of observing channels. Real clients contain code that is specific to channel types.

> 모든 채널에 관심이 있다는 것을 나타내는 필터를 제공할 수도 있지만, 실제로는 채널 관찰에 대한 예시로서만 쓸모가 있습니다. 실제 클라이언트들은 채널 타입에 종속적인 코드를 가집니다.

> An empty filter indicates a Handler is not interested in any channel types. However it is still possible to dispatch a channel to this handler if you do so by name. Temporary Handlers which are created on demand to handle a specific channel use such a filter.

> 빈 필터는 Handler가 어떤 채널 타입에도 관심이 없다는 것을 나타냅니다. 하지만 이름을 통해 배포한다면 여전히 채널들을 이러한 핸들러에 배포할 수 있습니다. 특정 채널을 다루기 위해 생성되는 임시 Handler들이 이러한 필터를 사용합니다.

## 20.4. The Role of Language Bindings

## 20.4. 언어 바인딩의 역할

As Telepathy is a D-Bus API, and thus can driven by any programming language that supports D-Bus. Language bindings are not required for Telepathy, but they can be used to provide a convenient way to use it.

Telepathy는 D-Bus API이므로, D-Bus를 지원하는 어떠한 프로그래밍 언어로도 운용될 수 있습니다. Telepathy가 언어 바인딩을 요구하진 않지만, 있으면 Telepathy를 편리하게 사용할 수 있습니다.

Language bindings can be split into two groups: low-level bindings that include code generated from the specification, constants, method names, etc.; and high-level bindings, which are hand-written code that makes it easier for programmers to do things using Telepathy. Examples of high-level bindings are the GLib and Qt4 bindings. Examples of low-level bindings are the Python bindings and the original libtelepathy C bindings, though the GLib and Qt4 bindings include a low-level binding.

언어 바인딩들은 두 개의 그룹으로 나눌 수 있습니다: 명세, 상수, 메서드 이름 등으로부터 생성된 코드를 포함하는 저수준 바인딩, 그리고 프로그래머들이 Telepathy를 응용하여 개발할 수 있기 쉽게 손으로 쓰인 고수준 바인딩이 있습니다. 고수준 바인딩의 예로는 Glib와 Qt4 바인딩이 있습니다. 저수준 바인딩의 예로는 파이썬 바인딩과 기존의 libtelepathy C 바인딩이 있지만, GLib와 Qt4 바인딩도 저수준 바인딩을 포함합니다.

### 20.4.1. Asynchronous Programming

### 20.4.1. 비동기 프로그래밍

Within the language bindings, all method calls that make requests over D-Bus are asynchronous: the request is made, and the reply is given in a callback. This is required because D-Bus itself is asynchronous.

언어 바인딩에서 D-Bus로 요청을 보내는 모든 메서드 호출들은 응답이 콜백으로 주어지는 비동기적 방식으로 동작합니다. D-Bus 자체가 비동기식이므로 이런 동작 방식이 요구됩니다.

Like most network and user interface programming, D-Bus requires the use of an event loop to dispatch callbacks for incoming signals and method returns. D-Bus integrates well with the GLib mainloop used by the GTK+ and Qt toolkits.

대부분의 네트워크 및 사용자 인터페이스 프로그래밍과 같이, D-Bus는 들어오는 시그널과 메서드 반환에 대한 콜백 발생을 위해 이벤트 루프의 사용을 필요로 합니다. D-Bus는 GTK+와 Qt 툴킷들이 사용하는 GLip mainloop와 잘 통합됩니다.

Some D-Bus language bindings (such as dbus-glib) provide a pseudo-synchronous API, where the main loop is blocked until the method reply is returned. Once upon a time this was exposed via the telepathy-glib API bindings. Unfortunately using pseudo-synchronous API turns out to be fraught with problems, and was eventually removed from telepathy-glib.

> Why Pseudo-Synchronous D-Bus Calls Don't Work

> 가성 비동기 D-Bus 호출을 쓸 수 없는 이유

> The pseudo-synchronous interface offered by dbus-glib and other D-Bus bindings is implemented using a request-and-block technique. While blocking, only the D-Bus socket is polled for new I/O and any D-Bus messages that are not the response to the request are queued for later processing.

> 가성 비동기 인터페이스는 요청 후 블러킹하는 기법으로 작성되어 있습니다. 블러킹하는 도중엔, D-Bus 소켓만이 새로운 I/O를 위해 폴링되며, 해당 요청에 대한 응답이 아닌 D-Bus 메시지들은 나중에 처리하기 위해 큐에 쌓입니다.

> This causes several major and inescapable problems:

> 이것은 몇 가지 회피할 수 없는 주요 문제를 야기합니다:

> * The caller is blocked while waiting for the request to be answered. It (and its user interface, if any) will be completely unresponsive. If the request requires accessing the network, that takes time; if the callee has locked up, the caller will be unresponsive until the call times out. 
Threading is not a solution here because threading is just another way of making your calling asynchronous. Instead you may as well make asynchronous calls where the responses come in via the existing event loop.
* Messages may be reordered. Any messages received before the watched-for reply will be placed on a queue and delivered to the client after the reply. 
This causes problems in situations where a signal indicating a change of state (i.e., the object has been destroyed) is now received after the method call on that object fails (i.e., with the exception `UnknownMethod`). In this situation, it is hard to know what error to display to the user. Whereas if we receive a signal first, we can cancel pending D-Bus method calls, or ignore their responses.
* Two processes making pseudo-blocking calls on each other can deadlock, with each waiting for the other to respond to its query. This scenario can occur with processes that are both a D-Bus service and call other D-Bus services (for example, Telepathy clients). The Channel Dispatcher calls methods on clients to dispatch channels, but clients also call methods on the Channel Dispatcher to request the opening of new channels (or equally they call the Account Manager, which is part of the same process).

> * 호출자는 요청에 대한 응답을 받을 때 까지 블럭되며, 호출자(존재한다면 호출자의 사용자 인터페이스 역시)는 완전히 무반응 상태가 됩니다. 요청이 네트워크 이용을 필요로 하면, 이것은 시간이 걸리고, 피호출자에 락이 걸린 상태라면 호출이 타임아웃이 날 때 까지 무반응 상태를 유지하게 됩니다.
쓰레드를 만드는 것 역시 비동기식 호출의 또다른 방식이므로 해결책이 되지 않습니다. 차라리 응답이 기존 이벤트 루프를 통해 들어오는 비동기 호출을 사용하는 것이 낫습니다. 
* 메시지들이 재배치될 수 있습니다. watched-for 응답 이전에 수신된 메시지들은 큐에 쌓이게 되며 응답 이후에 클라이언트에 전달되게 됩니다.
이것은 상태 변경에 대한 시그널(객체가 소멸됨)이 해당 객체에 대한 메서드 호출이 실패한 이후(`UnknownMethod` 예외와 함께)에 들어오게 되는 상황에서 문제가 됩니다. 이 상황에서는, 사용자에게 어떤 오류 메시지를 보여줘야 할지 모호하게 됩니다. 반면, 시그널을 먼저 수신하게 된다면, 대기중인 D-Bus 메서드 호출을 취소하거나 반환값을 무시할 수 있습니다. 
* 서로에게 가성 비동기 호출을 보내는 두 프로세스는 서로의 쿼리에 대한 응답을 기다리는 데드락을 만들 수 있습니다. 이 상황은 다른 D-Bus 서비스를 호출하는 두 프로세스가 모두 D-Bus 서비스일 경우에 생길 수 있습니다(e.g., Telepathy 클라이언트). Channel Dispathcer는 채널을 배포하기 위해 클라이언트의 메서드를 호출하지만, 클라이언트들 역시 새로운 채널의 생성 요청을 위해 Channel Dispatcher의 메서드를 호출합니다(같은 과정 중 하나인, Account Manager을 호출할 수도 있습니다). 

Method calls in the first Telepathy bindings, generated in C, simply used typedef callback functions. Your callback function simply had to implement the same type signature.

C로 생성된 초기 Telepathy 바인딩들의 메서드 호출은 단순히 typedef 콜백 함수들을 사용하였습니다. 콜백 함수는 같은 타입 시그니쳐를 구현하기만 하면 되었습니다.

~~~
typedef void (*tp_conn_get_self_handle_reply) (
    DBusGProxy *proxy,
    guint handle,
    GError *error,
    gpointer userdata
);
~~~

This idea is simple, and works for C, so was continued into the next generation of bindings.

이 아이디어는 단순하고 C에 대해 동작하므로 다음 세대의 바인딩에도 포함되었습니다.

In recent years, people have developed a way to use scripting languages such as Javascript and Python, as well as a C#-like language called Vala, that use GLib/GObject-based APIs via a tool called GObject-Introspection. Unfortunately, it's extremely difficult to rebind these types of callbacks into other languages, so newer bindings are designed to take advantage of the asynchronous callback features provided by the languages and GLib.

최근 몇 년 간, 사람들은 GObject-Introspection이라는 GLib/GObject 기반의 API를 통해 자바스크립트나 파이썬, C#과 유사한 언어인 Vala 같은 스크립팅 언어를 사용하기 시작했습니다. 안타깝게도, 이러한 타입의 콜백을 다른 언어로 바인딩 하는 것은 매우 힘들기 때문에, 새로운 바인딩들은 해당 언어와 GLib에서 제공하는 비동기 콜백 기능을 사용하도록 설계되었습니다.

### 20.4.2. Object Readiness

### 20.4.2. 객체의 준비성

In a simple D-Bus API, such as the low-level Telepathy bindings, you can start making method calls or receive signals on a D-Bus object simply by creating a proxy object for it. It's as simple as giving an object path and interface name and getting started.

저수준 Telepathy 바인딩같은 간단한 D-Bus API에서는 단순히 프록시 객체를 만들어 D-Bus 객체의 메서드를 호출하거나 시그널을 받을 수 있습니다. 객체 경로와 인터페이스 이름을 주는 것만으로도 할 수 있습니다.

However, in Telepathy's high-level API, we want our object proxies to know what interface are available, we want common properties for the object type to be retrieved (e.g., the channel type, target, initiator), and we want to determine and track the object's state or status (e.g., the connection status).

하지만, Telepathy의 고수준 API에서는 객체 프록시가 이용할 수 있는 인터페이스에 대해 알기를 원하기 때문에 객체 타입에 대한 공통 속성들(e.g., 채널 타입, 타겟, 창시자 등)을 가져와야 하며, 객체의 상태(e.g., 연결 상태)를 판단하고 추적할 수 있어야 합니다.

Thus, the concept of readiness exists for all proxy objects. By making a method call on a proxy object, you are able to asynchronously retrieve the state for that object and be notified when state is retrieved and the object is ready for use.

따라서, 모든 프록시 객체에 대해서는 준비성이라는 개념이 존재합니다. 프록시 객체에 메서드 호출을 함으로서 해당 객체의 상태를 비동기적으로 받아오고, 객체를 사용할 수 있을 때 통보를 받을 수 있습니다.

Since not all clients implement, or are interested in, all the features of a given object, readiness for an object type is separated into a number of possible features. Each object implements a core feature, which will prepare crucial information about the object (i.e., its Interfaces property and basic state), plus a number of optional features for additional state, which might include extra properties or state-tracking. Specific examples of additional features you can ready on various proxies are contact info, capabilities, geolocation information, chat states (such as "Escher is typing…") and user avatars.

모든 클라이언트가 해당 객체의 모든 기능에 관심이 있는 것이 아니기 때문에, 객체의 준비성은 몇 가지 기능으로 나뉘어져 있습니다. 각 객체는 객체에 대한 중요한 정보를(객체의 Interfaces 속성과 기본 상태) 준비하는 핵심 기능과, 별도의 속성이나 상태 추적 등 추가적인 상태들에 대한 몇 가지 선택적 기능을 구현합니다. 여러 프록시에 대해 준비할 수 있는 추가적 기능의 예로는 연락처 정보, 기능, 위치 정보, 대화 상태(상대방의 타이핑 상태 등), 그리고 사용자 아바타 등이 있습니다.

For example, connection object proxies have:

예를 들어, 연결 객체 프록시들은 다음을 가지고 있습니다:

* a core feature which retrieves the interface and connection status;
* features to retrieve the requestable channel classes and support contact info; and
* a feature to establish a connection and return ready when connected.

* 인터페이스와 연결 상태를 가져오는 핵심 기능
* 요청 가능한 채널 클래스와 지원 연락처 정보
* 연결을 확립하고 준비 상태를 반환하는 기능

The programmer requests that the object is readied, providing a list of features in which they are interested and a callback to call when all of those features are ready. If all the features are already ready, the callback can be called immediately, else the callback is called once all the information for those features is retrieved.

프로그래머는 관심 있는 기능들의 목록과 기능들이 준비되었을 때 호출할 콜백과 함께 객체 준비 요청을 보냅니다. 모든 기능들이 준비되면 콜백은 호출되며, 이미 모든 기능들이 준비되어 있을 경우 콜백은 즉시 호출됩니다. 

## 20.5. 견고성

Telepathy의 주요 이점은 Telepathy의 견고성입니다. Telepathy의 구성 요소들은 모듈화되어 있으므로 하나의 구성 요소가 고장나도 전체 시스템이 중단되지 않습니다. 다음은 Telepathy를 견고하게 만드는 몇 가지 특징들입니다:

* Account Manager와 Channel Dispatcher는 상태를 회복할 수 있습니다. Mission Control(Account Manager와 Channel Dispatcher를 포함하는 하나의 프로세스)이 시작할 때, 사용자의 세션 버스에 등록되어 있는 서비스들의 이름을 확인합니다. 알려진 계정과 연관된 Connection을 발견하면 (새로운 연결을 만드는 대신) 다시 해당 계정과 연관시키며, 실행 중인 클라이언트들이 처리 하고 있는 채널의 목록을 가져옵니다.
* 클라이언트가 채널을 처리하는 도중에 사라질 경우에 Channel Dispatcher는 클라이언트를 재실행시고 채널을 다시 등록합니다.
클라이언트가 반복적으로 중단될 경우엔 Channel Dispatcher는 다른 클라이언트를 실행할 수 있으며, 다른 클라이언트가 없을 경우엔 (클라이언트가 처리할 수 없는 데이터에 의해 반복적으로 중단되는 것을 막기 위해) 채널을 닫습니다.
텍스트 메시지는 대기 큐에서 빠지기 전에 승인되어야 합니다. 클라이언트는 사용자가 메시지를 본 후에야(메시지 창에 포커스를 주는 등) 메시지를 승인할 수 있습니다. 이를 통해 클라이언트가 메시지를 렌더링하려는 도중에 중단된 경우에도 채널은 대기 메시지 큐에 표시하지 못한 메시지에 대한 정보를 가지고 있을 수 있습니다.
* Connection이 중단될 경우엔, Account Manager는 Connection을 다시 만듭니다. 이 과정에서 채널의 상태는 사라지지만, 해당 프로세스의 Connection에만 영향을 미칩니다. 클라이언트들은 연결들의 상태를 관찰할 수 있으며, 연락처 목록과, 다른 상태 없는 채널들에 대한 정보 등을 다시 요청하기만 하면 됩니다.

## 20.6. Extending Telepathy: Sidecars

## 20.6. Telepathy 확장하기: Sidecar

Although the Telepathy specification tries to cover a wide range of features exported by communication protocols, some protocols are themselves extensible4. Telepathy's developers wanted to make it possible extend your Telepathy connections to make use of such extensions without having to extend the Telepathy specification itself. This is done through the use of sidecars.

Telepathy 명세는 통신 프로토콜들이 노출하는, 넓은 영역의 기능을 포함하려고 하지만, 어떤 프로토콜들은 프로토콜 자체가 확장될 수 있습니다. Telepathy의 개발자들은 Telepathy 명세를 확장하지 않고도 연결을 확장할 수 있게 하고 싶었으며, 이것은 사이드카를 통해 가능합니다.

Sidecars are typically implemented by plugins in a Connection Manager. Clients call a method requesting a sidecar that implements a given D-Bus interface. For example, someone's implementation of XEP-0016 privacy lists might implement an interface named com.example.PrivacyLists. The method then returns a D-Bus object provided by the plugin, which should implement that interface (and possibly others). The object exists alongside the main Connection object (hence the name sidecar, like on a motorcycle).

사이드카는 일반적으로 Connection Manager의 플러그인에 의해 구현됩니다. 클라이언트들은 특정 D-Bus 인터페이스를 구현하는 사이드카를 요청하는 메서드를 호출합니다. 예를 들어, 어떤 사람의 XEP-0016 개인 정보 목록의 구현체는 `com.example.PrivacyLists`라는 인터페이스를 구현할 수 있습니다. 해당 메서드는 해당 인터페이스를 구현하는(추가적으로 다른 인터페이스를 구현할 수도 있는) 플러그인이 제공하는 D-Bus 객체를 반환합니다. 해당 객체는 메인 Connection 객체와 공존하게 됩니다(이 때문에 오토바이의 사이드카라는 이름을 가지게 되었습니다).

> The History of Sidecars

> Sidecar의 역사

> In the early days of Telepathy, the One Laptop Per Child project needed to support custom XMPP extensions (XEPs) to share information between devices. These were added directly to Telepathy-Gabble (the XMPP Connection Manager), and exposed via undocumented interfaces on the Connection object. Eventually, with more developers wanting support for specific XEPs which have no analogue in other communications protocols, it was agreed that a more generic interface for plugins was needed.

> 옛날 Telepathy 버전에서는, One Laptop Per Child 프로젝트는 기기 간 정보를 공유하기 위해 맞춤형 XMPP 확장(XEP)을 지원할 필요가 있었습니다. 이 확장들은 Telepathy-Gabble(XMPP 연결 매니저)에 직접 추가되었으며, 문서화되지 않은 인터페이스로서 Connection 객체에 추가되었습니다. 결과적으로, 다른 통신 프로토콜과 대응되는 것이 없는, 특정 XEP에 대한 지원을 원하는 개발자들이 많아지며, 플러그인에 대한 일반화된 인터페이스의 필요성이 인정되었습니다.

## 20.7. A Brief Look Inside a Connection Manager

## 20.7. Connection Manager 내부 개요

Most Connection Managers are written using the C/GLib language binding, and a number of high-level base classes have been developed to make writing a Connection Manager easier. As discussed previously, D-Bus objects are published from software objects that implement a number of software interfaces that map to D-Bus interfaces. Telepathy-GLib provides base objects to implement the Connection Manager, Connection and Channel objects. It also provides an interface to implement a Channel Manager. Channel Managers are factories that can be used by the BaseConnection to instantiate and manage channel objects for publishing on the bus.

대부분의 Connection Manager들은 C/GLib 언어 바인딩을 통해 작성되었으며, Connection Manager 작성을 간편하게 하기 위해 몇 가지 고수준 기반 클래스가 개발되어 있습니다. 이전에 논의되었던 것 처럼, D-Bus 객체들은 D-Bus 인터페이스에 매핑되는 몇 가지 소프르웨어 인터페이스를 구현하는 소프트웨터 객체에서 발행됩니다. Telepathy-GLib은 Connection Manager, Connection, 그리고 Connection 객체를 구현하기 위한 기반 객체를 제공합니다. Channel Manager들은 BaseConnection에 의해 버스에 발행하기 위한 채널 객체를 초기화하고 관리하기 위해 사용될 수 있는 팩토리입니다.

The bindings also provide what are known as mixins. These can be added to a class to provide additional functionality, abstract the specification API and provide backwards compatibility for new and deprecated versions of an API through one mechanism. The most commonly used mixin is one that adds the D-Bus properties interface to an object. There are also mixins to implement the `ofdT.Connection.Interface.Contacts` and `ofdT.Channel.Interface.Group` interfaces and mixins making it possible to implement the old and new presence interfaces, and old and new text message interfaces via one set of methods.

바인딩들은 믹스인을 제공합니다. 믹스인들은 추가적인 기능을 제공하거나, 명세 API의 새로운 버전이나 더 이상 권장되지 않는 버전의 API에 대한 하위 호환성을 하나의 체계를 통해 제공하는 추상화를 클래스에 추가할 수 있습니다. 가장 일반적으로 사용되는 믹스인은 오브젝트에 D-Bus 속성 인터페이스를 추가하는 믹스인입니다. `ofdT.Connection.Interface.Contacts`와 `ofdT.Channel.Interface.Group` 인터페이스를 구현하는 믹스인들도 있으며, 이 믹스인을 통해 예전과 현재의 존재 여부 인터페이스와 텍스트 메시지 인터페이스를 하나의 메서드 집합을 통해 구현할 수 있게 되었습니다.

![Example Connection Manager Architecture](http://aosabook.org/images/telepathy/cm.png)

![Connection Manager 설계 예시](http://aosabook.org/images/telepathy/cm.png)

Figure 20.5: Example Connection Manager Architecture

그림 20.5: Connection Manager 설계 예시

> Using Mixins to Solve API Mistakes

> 믹스인을 통한 API 설계 실수 해결하기

> One place where mixins have been used to solve a mistake in the Telepathy specification is the `TpPresenceMixin`. The original interface exposed by Telepathy (`odfT.Connection.Interface.Presence`) was incredibly complicated, hard to implement for both Connections and Clients, and exposed functionality that was both nonexistent in most communications protocols, and very rarely used in others. The interface was replaced by a much simpler interface (`odfT.Connection.Interface.SimplePresence`), which exposed all the functionality that users cared about and had ever actually been implemented in the connection managers.

믹스인이 Telepathy 명세의 실수를 해결하는 데 사용된 곳 중 하나는 `TpPresenceMixin`입니다. Telepathy에 의해 노출되던 기존 인터페이스(`odfT.Connection.Interface.Presence`)는 Connection에게나 Client에게나 매우 복잡하고 구현하기 힘들었으며, 대부분의 통신 프로토콜에는 존재하지 않거나 거의 사용되지 않는 기능을 노출했습니다. 이 인터페이스는 사용자들이 필요로 하는 모든 기능들을 노출하고, 실제로 연결 관리자에서 구현된 훨씬 간단한 인터페이스(`odfT.Connection.Interface.SimplePresence`)로 교체되었습니다.

> The presence mixin implements both interfaces on the Connection so that legacy clients continue to work, but only at the functionality level of the simpler interface.

존재 여부 믹스인은 옛날 클라이언트들이 계속 동작할 수 있도록 Connection에 두 인터페이스 모두 구현하지만, 단순한 인터페이스 쪽의 기능 수준만을 구현합니다.

## 20.8. Lessons Learned

## 20.8. 얻은 교훈

Telepathy is an excellent example of how to build a modular, flexible API on top of D-Bus. It shows how you can develop an extensible, decoupled framework on top of D-Bus. One which requires no central management daemon and allows components to be restartable, without loss of data in any other component. Telepathy also shows how you can use D-Bus efficiently and effectively, minimizing the amount of traffic you transmit on the bus.

Telepathy는 D-Bus 위에서 모듈화된, 유연한 API를 만든 훌륭한 예시입니다. D-Bus 위에서, 중앙 관리 데몬을 필요로 하지 않고, 구성 요소들이 개별적으로, 다른 구성 요소의 데이터 손실 없이, 재시작될 수 있는 유연하고 분산된 프레임워크를 개발할 수 있다는 것을 보여줍니다. 또, Telepathy는 버스에 전송하는 트래픽을 최소화시켜 D-Bus를 효율적이고 효과적으로 사용할 수 있는 방식도 보여줍니다.

Telepathy's development has been iterative, improving its use of D-Bus as time goes on. Mistakes were made, and lessons have been learned. Here are some of the important things we learned in designing the architecture of Telepathy:

Telepathy는 D-Bus를 사용하는 방식 개선의 반복을 통해 개발되었습니다. 실수도 있었지만, 그에 따른 교훈도 얻었습니다. 다음은 Telepathy를 설계하며 얻은 몇 가지 중요한 교훈들입니다:

* Use D-Bus properties; don't require dozens of small D-Bus method calls to look up information. Every method call has a round-trip time. Rather than making lots of individual calls (e.g., `GetHandle`, `GetChannelType`, `GetInterfaces`) use D-Bus properties and return all the information via a single call to `GetAll`.
* Provide as much information as you can when announcing new objects. The first thing clients used to do when they learned about a new object was to request all of its properties to learn whether they were even interested in the object. By including the immutable properties of an object in the signal announcing the object, most clients can determine their interest in the object without making any method calls. Furthermore, if they are interested in the object, they do not have to bother requesting any of its immutable properties.
* The Contacts interface allows requesting information from multiple interfaces at once. Rather than making numerous `GetAll` calls to retrieve all the information for a contact, the Contacts interface lets us request all the information at once, saving a number of D-Bus round trips.
* Don't use abstractions that don't quite fit. Exposing the contact roster and contact groups as channels implementing the Group interface seemed like a good idea because it used existing abstractions rather than requiring additional interfaces. However, it made implementing clients difficult and was ultimately not suitable.
* Ensure your API will meet your future needs. The original channel requesting API was very rigid, only permitting very basic channel requests. This did not meet our needs when needing to request channels that required more information. This API had to be replaced with one that had significantly more flexibility.

* D-Bus 속성을 사용한다; 정보를 가져오기 위해 수십개의 작은 D-Bus 메서드 호출을 필요로 하지 않게 한다. 모든 메서드 호출에는 왕복 시간이 있습니다. 많은 개별 호출(`GetHandle`, `GetChannelType`, `GetInterfaces` 등)을 하는 대신 D-Bus 속성을 이용하고 하나의 `GetAll` 호출을 통해 정보를 가져 온다.
* 새로운 객체를 선언할 때엔 최대한 많은 정보를 제공한다. 클라이언트가 제일 먼저 하는 일은, 해당 객체가 필요하긴 한지 알아내기 위해 해당 객체에 대한 모든 속성을 요청하는 것입니다. 객체의 불변 속성을 객체 선언 시그널에 포함시킴으로서 대부분의 클라이언트는 메서드 호출을 하지 않고서도 객체가 필요한지 판단할 수 있습니다. 또, 객체가 필요하다고 판단 될 경우에도 불변 속성에 대한 요청을 보낼 필요가 없어집니다.
* Contacts 인터페이스는 여러 인터페이스로부터의 정보를 한번에 가져올 수 있게 합니다. 연락처에 대한 정보를 가져오기 위해 `GetAll`을 여러 번 하는 것이 아니라, Contacts 인터페이스는 모든 정보에 대한 요청을 보낼 수 있게 하여, D-Bus에 왕복 요청을 보내는 횟수를 줄일 수 있습니다.
* 잘 맞지 않는 추상화를 사용하지 않는다. 연락처 목록과 연락처 그룹을 Group 인터페이스를 구현하는 채널로서 노출시키는 것은, 기존의 추상화를 사용하기 때문에 처음에는 좋은 아이디어 같아 보였지만, 클라이언트 구현을 어렵게 만들었으며, 궁극적으로는 적절하지 않았습니다.
* API가 미래의 요구 사항을 충족시킬 수 있도록 보장하라. 기존의 채널 요청 API는 단순한 채널 요청만 보낼 수 있게 하는 등, 매우 엄격했습니다. 이것은 더 많은 정보를 필요로 하는 채널을 요청할 때 우리의 요구 사항에 맞출 수 없었습니다. 이 API는 결국 더 유연한 새로운 API로 교체되어야 했습니다.
