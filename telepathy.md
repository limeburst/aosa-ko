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
