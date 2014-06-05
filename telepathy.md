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
