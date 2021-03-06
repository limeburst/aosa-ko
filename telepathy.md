# Telepathy

Telepathy[^1]는 음성, 영상, 텍스트, 파일 전송 등을 다루는 실시간 통신을 위한 모듈화된 프레임워크입니다. Telepathy의 차별점은 다양한 인스턴트 메시지 프로토콜의 세부사항을 추상화 한다는 점이 아니라, 여러 응용 프로그램이 동시에 사용하는 프린터 서비스처럼, 통신을 하나의 서비스로써 제공한다는 점입니다. Telepathy는 이것을 달성하기 위해 D-Bus 메시지 버스와 모듈화된 설계를 광범위하게 사용합니다.

서비스로서의 통신은 응용 프로그램 간의 통신 수단을 제공하므로 굉장히 유용합니다. 서비스로서의 통신은, 이메일 클라이언트에서 연락처의 상태를 확인하고, 해당 연락처와 통신을 시작하고, 파일 브라우저에서 바로 파일을 전송하거나, Telepathy에서 Tubes로 알려진 기능인 응용 프로그램 내에서 연락처 간의 협업 기능 제공 등, 흥미로운 많은 일을 가능하게 합니다. 

Telepathy는 2005년 로버트 맥퀸(Robert McQueen)이 만들었으며, 그 이후 맥퀸이 공동 창립한 회사인 Collabora를 포함한 여러 회사와 개인이 유지, 개발하고 있습니다.

> D-Bus 메시지 버스

> D-Bus는 GNOME, KDE 데스크톱 환경 등, GNU/Linux 시스템의 백본 대부분을 구성하는, 프로세스 간 통신을 위한 비동기적 메시지 버스입니다. D-Bus의 설계는 공유 버스를 기반으로 합니다. 응용 프로그램들은 (소켓 주소로 구분되는) 버스에 연결하여 같은 버스에 연결된 다른 응용 프로그램을 대상으로 메시지를 보내거나 모든 버스 구성원에게 광대역(broadcast) 신호를 보낼 수 있습니다. 버스에 연결된 응용 프로그램에는 IP 주소와 유사한 버스 주소가 할당되고, DNS 이름처럼 `org.freedesktop.Telepathy.AccountManager` 같은 몇 개의 잘 알려진 이름을 차지할 수 있습니다. 모든 프로세스는, 메시지 전달과 이름 등록을 처리하는, D-Bus 데몬을 통해 통신합니다.

> 사용자의 관점에서 볼 때, 모든 시스템에는 두 개의 버스가 있습니다. 시스템 버스는 사용자가 시스템 공용의 구성요소(프린터, 블루투스, 하드웨어 관리 등)들과 통신하게 해 주며, 시스템을 사용하는 모든 사용자와 공유됩니다. 세션 버스는 사용자에게 고유한, 즉, 로그인된 사용자당 하나의 세션 버스가 있으며, 사용자의 각 응용 프로그램이 서로 통신을 할 때 사용됩니다. 응용 프로그램이 대량의 트래픽을 버스를 통해 전달해야 하는 경우, 사설 버스나, 중재자인 `dbus-daemon`이 없는 P2P 버스를 생성하여 통신할 수도 있습니다.

> libdus, GDBus, QtDBus, python-dbus 등 여러 라이브러리가 D-Bus 데몬과 통신하기 위한 D-Bus 프로토콜을 구현합니다. 이 라이브러리들은 D-Bus 메시지의 송수신, 언어의 타입을 D-Bus의 타입으로 마샬링, 그리고 객체를 버스에 발행하는 역할을 합니다. 이러한 라이브러리들은 주로, 연결됐거나 활성화 가능한 응용 프로그램의 목록을 받아오거나, 버스에서 잘 알려진 이름들을 요청하는 편의성 API도 제공합니다. D-Bus 단에서 이 모든 것은 `dbus-daemon` 자체가 발행한 객체의 메서드를 호출하여 이루어집니다.

> D-Bus에 대한 더 자세한 정보는 [http://www.freedesktop.org/wiki/Software/dbus](http://www.freedesktop.org/wiki/Software/dbus) 에 있습니다.

## 20.1. Telepathy 프레임워크의 구성요소

Telepathy는 모듈화되어 있으며, 각 모듈들은 D-Bus 메시징 버스를 통해 통신합니다. 대부분의 모듈은 사용자 세션 버스를 사용합니다. 이 통신은 Telepathy 명세[^2]에 상세히 명시되어 있습니다. 그림 20.1에 Telepathy 프레임워크의 구성요소들이 나와 있습니다.

![Telepathy 구성요소 예시](http://aosabook.org/images/telepathy/telepathy-components.png)

* 연결 관리자는 Telepathy와 통신 서비스들 간의 인터페이스를 제공합니다. XMPP, SIP, IRC 등을 위한 연결 관리자가 있습니다. 새로운 프로토콜에 대한 지원을 위해서는 해당 프로토콜을 위한 새로운 연결 관리자를 작성하면 됩니다.
* 계정 관리자 서비스는 사용자의 통신 계정들을 저장하고, 요청을 적합한 연결 관리자에 연결하는 역할을 합니다.
* 채널 배포자는 각 연결 관리자로부터 들어오는 채널을 듣고, 해당 종류의 채널(문자, 음성, 영상, 파일, 튜브 등)을 다룰 수 있다고 알린 클라이언트들에게 전달합니다. 채널 배포자는 특히 Telepathy 클라이언트가 아닌 응용 프로그램이 발송 채널을 요청하고 적절한 클라이언트가 그것을 지역적으로 처리할 수 있게 하는 서비스를 제공합니다. 이것은 응용 프로그램, 예를 들어 이메일 클라이언트가 연락처와의 텍스트 채팅을 요청하면, 인스턴스 메시징 클라이언트가 채팅 창을 보여주게 할 수 있습니다.
* Telepathy 클라이언트들은 들어오는 채널(문자, 음성, 영상, 파일, 튜브 등)에 대한 연결 관리자의 신호를 듣고, 해당 채널을 처리할 수 있는 클라이언트들에게 전달합니다. 클라이언트는 인스턴스 메신저와 VoIP 클라이언트 같은 사용자 인터페이스 그리고 대화 로거 같은 서비스를 모두 포함합니다. 클라이언트는 관심 있거나 처리하고자 하는 채널 종류의 목록과 함께 자신을 채널 배포자에 등록합니다.

현재 버전의 Telepathy에서는, 계정 관리자와 채널 배포자는 Mission Control이라는 하나의 프로세스가 제공하도록 구현되어 있습니다.

이러한 모듈화는 더그 맥일로이의 "딱 한 가지 일만을 훌륭하게 처리하는 프로그램을 작성한다"라는 철학에 기반하였고, 몇 가지 중요한 이점을 가집니다:

* 견고함: 한 구성요소에 결함이 있다고 해서 전체 서비스를 무너지게 하지 않습니다.
* 개발의 편리함: 동작 중인 시스템의 구성요소들은 다른 구성요소에 영향을 주지 않으면서 교체될 수 있습니다. 개발 중인 모듈을 안정된 버전의 모듈과 비교하며 테스트할 수도 있습니다.
* 언어 독립성: 구성요소들은 D-Bus 바인딩이 있는 어떠한 언어로도 작성될 수 있습니다. 주어진 커뮤니케이션 프로토콜의 가장 좋은 구현체가 특정 언어로 작성되었다면, 해당 언어로 연결 관리자를 작성할 수 있으며, 그 연결 관리자는 모든 Telepathy 클라이언트에서 사용될 수 있습니다. 비슷한 맥락에서, 어떤 언어로 사용자 인터페이스를 개발하든, 이용할 수 있는 프로토콜에 대한 제한이 없습니다.
* 라이센스 독립성: 시스템이 하나의 프로세스로 동작한다면 라이센스 호환이 안 되겠지만, 서로 별개인 구성요소로 이루어져 있기 때문에 구성요소들은 서로 다른 소프트웨어 라이센스를 가질 수 있습니다.
* 인터페이스 독립성: 같은 Telepathy 구성요소를 기반으로 다양한 사용자 인터페이스를 개발할 수 있습니다. 이것은 데스크톱 환경과 하드웨어 장치를 위한 네이티브 인터페이스 구현을 가능하게 합니다(GNOME, KDE, Meego, Sugar 등).
* 보안: 구성요소들은 각자의 주소공간에서 매우 제한된 권한을 가지고 실행됩니다. 예를 들어, 전형적인 연결 관리자는 네트워크와 D-Bus 세션 버스에 대한 접근 권한만을 필요로 하며, SELinux 같은 모듈을 사용하여 구성요소의 자원 접근 권한을 제한할 수 있습니다.

연결 관리자는 여러 개의 연결을 관리하며, 각 연결은 통신 서비스와의 논리적인 연결을 나타냅니다. 설정된 계정당 하나의 연결이 존재하며, 하나의 연결은 여러 개의 채널을 포함합니다. 채널은 통신이 이루어지는 메커니즘이며, 인스턴스 메신저 대화, 음성, 영상 통화, 파일 전송, 혹은 다른 상태를 유지해야 하는 작업일 수 있습니다. 연결과 채널에 대해서는 20.3장에서 자세히 다룹니다.

## 20.2. Telepathy가 D-Bus를 사용하는 방식

Telepathy 구성요소들은 D-Bus 메시징 버스를 통해 통신하며, 주로 사용자의 세션 버스를 사용합니다. D-Bus는 다양한 IPC 시스템에서 공통적으로 찾아볼 수 있는 기능을 제공합니다. 서비스는 `/org/freedesktop/Telepathy/AccountManager`[^3]처럼, 엄격한 이름 공간의 객체 경로를 가진 객체를 발행하며, 각 객체는 몇 가지 인터페이스를 구현합니다. 이 인터페이스들 역시 `org.freedesktop.DBus.Properties` 그리고 `ofdT.Connection` 같은 형식의 엄격한 이름 공간을 가지며, 각 인터페이스는 호출, 듣기, 또는 요청 가능한 메서드와 시그널, 그리고 속성들을 제공합니다.

![D-Bus 서비스가 발행한 객체들의 개념적 표현](http://aosabook.org/images/telepathy/bus-hierarchy-conceptual.png)

> D-Bus 객체 발행하기

> D-Bus 객체의 발행은 사용되는 D-Bus 라이브러리에 의해 온전히 처리됩니다. 결과적으로 볼 때, 객체 발행은 D-Bus 객체 경로를 해당되는 인터페이스를 구현하는 소프트웨어 객체로 대응시키는 것입니다. 서비스가 발행하는 객체의 경로는 `org.freedesktop.DBus.Introspectable`이라는 선택적인 인터페이스에 의해 노출됩니다.

> 서비스가 지정된 목적지 경로(`/ofdT/AccountManager` 등)와 함께 메서드 호출을 받으면, D-Bus 라이브러리는 해당 D-Bus 객체를 제공하는 소프트웨어 객체를 찾고, 찾은 객체에 대한 적절한 메서드 호출을 하는 역할을 합니다.

Telepathy가 제공하는 인터페이스, 메서드, 시그널 그리고 속성들은, 더 많은 정보를 포함할 수 있도록 확장된 XML 기반의 D-Bus IDL로 명시되어 있습니다. Telepathy 명세는 구문 분석되어 문서와 언어 바인딩을 생성할 수 있습니다.

Telepathy 서비스들은 버스에 몇 가지 객체를 발행할 수 있습니다. Mission Control은 계정 관리자와 채널 배포자의 서비스에 접근하기 위한 객체를, 클라이언트들은 채널 배포자가 접근 가능한 Client 객체를 발행합니다. 연결 관리자는 계정 관리자가 새로운 연결들을 요청하기 위해 사용하는 서비스 객체, 열린 연결당 하나의 객체, 그리고 열린 채널당 하나의 객체를 발행합니다.

D-Bus 객체에는 (인터페이스만 있고) 타입이 없지만, Telepathy는 몇 가지 방법으로 타입을 흉내 냅니다. 객체의 경로는 객체가 연결인지, 채널인지 또는 클라이언트인지 등의 정보를 알려줍니다. 비록 대개는 객체에 대한 프락시를 요청할 때 이미 알지만 말입니다. 각 객체는 해당 타입의 기초 인터페이스를 구현합니다(`ofdT.Connection`, `ofdT.Channel` 등). 채널이 보기에 이 인터페이스는 추상화된 기반 클래스와 비슷합니다. 이제 채널 객체는 채널 타입을 정의하는 정확한 클래스를 가집니다. 이 역시 D-Bus 인터페이스에 의해 표현됩니다. 채널 타입은 채널 인터페이스의 `ChannelType` 속성을 읽어 알아낼 수 있습니다.

마지막으로, 각 객체는 프로토콜과 연결 관리자의 기능에 의존하는 몇 가지 선택적인 인터페이스를 구현합니다(놀랍지도 않지만, 이 역시 D-Bus 인터페이스에 의해 표현됩니다). 주어진 객체 위에서 제공되는 인터페이스들은 객체의 기반 클래스의 `Interface` 속성을 통해 접근할 수 있습니다.

`ofdT.Connection` 타입의 연결 객체의 선택적 인터페이스들은, (프로토콜에 아바타 개념이 있으면) `ofdT.Connection.Interface.Avatars`, (프로토콜이 연락처 목록을 제공한다면(모든 프로토콜이 제공하지는 않습니다)) `odfT.Connection.Interface.ContactList`, 그리고 (프로토콜이 위치 정보를 제공하면) `odfT.Connection.Interface.Location` 같은 이름을 가집니다. `ofdT.Channel` 타입을 가진 채널 객체에 대해서는, 구상 클래스는 `ofdT.Channel.Type.Text`, `odfT.Channel.Type.Call` 그리고 `odfT.Channel.Type.FileTransfer` 같은 형식의 인터페이스 이름을 가집니다. 연결과 비슷하게, 선택적 인터페이스는, (채널이 문자 메시지를 송수신 할 수 있으면) `odfT.Channel.Interface.Messages`, 그리고 (채널이 다수의 연락처를 포함하는 그룹을 대상으로 하면, 예를 들어 단체 채팅방) `odfT.Channel.Interface.Group` 같은 이름을 가집니다. 예를 들어, 텍스트 채널은 최소한 `ofdT.Channel`, `ofdT.Channel.Type.Text`, 그리고 `Channel.Interface.Messages` 인터페이스를 구현합니다. 단체 채팅방일 경우 `odfT.Channel.Interface.Group`도 구현합니다.

> D-Bus 인트로스펙션이 있는데 왜 Interface 속성을 사용하나요?

> 왜 기반 클래스가, 사용 가능한 인터페이스들 알아내는 데 D-Bus의 인트로스펙션 기능을 사용하지 않고, 각각의 `Interfaces` 속성을 구현하는지 궁금할 수도 있습니다. 서로 다른 채널과 커넥션 객체들은 갖고 있는 기능에 따라 다른 인터페이스를 제공할 수도 있습니다. 하지만 대부분의 D-Bus 인트로스펙션 구현체들은 같은 객체 클래스의 객체들은 모두 같은 인터페이스를 가진다고 가정합니다. 예를 들어, `telepathy-glib`에서 D-Bus 인트로스펙션이 찾은 인터페이스들은, 클래스가 구현하는 인터페이스들로부터 가져오며, 이것은 컴파일 시간에 정적으로 정의됩니다. 우리는 D-Bus 인트로스펙션이 객체에 존재할 수 있는 모든 인터페이스에 대한 정보를 제공하게 하고, `Interfaces` 속성이 객체에 실제로 존재하는 인터페이스들을 나타내게 하여 이 문제를 회피합니다.

D-Bus 자체에서는 커넥션 객체가 커넥션과 관련된 인터페이스만 가진다는 것을 보장하지 않습니다. D-Bus에는 임의 기명 인터페이스만 있고, 타입에 대한 개념은 존재하지 않기 때문입니다. 하지만 우리는 Telepathy 언어 바인딩 내에서, Telepathy 명세에 있는 정보를 사용하여 커넥션 객체가 정상적인 인터페이스를 가지는지 알 수 있습니다.

> IDL 명세가 왜, 어떻게 확장되었는지에 대해

> 기존 D-Bus IDL 명세는, 이름, 매개변수, 접근 권한, 메서드의 D-Bus 타입 시그니쳐, 속성, 그리고 시그널을 정의하였습니다. 문서, 바인딩 힌트 또는 기명 타입은 지원하지 않았습니다.

> 이 한계를 극복하기 위해, 필요한 정보를 제공하기 위한 새로운 XML 이름공간이 추가되었습니다. 이 이름공간은 다른 D-Bus API들도 사용할 수 있도록 일반화되어 설계되었습니다. 인라인 문서, 근거, 서론, 대체된 버전들, 그리고 메서드에서 발생될 수 있는 예외에 대한 정보를 포함하기 위한 요소들이 추가되었습니다.

> D-Bus 타입 시그니쳐는 버스 위에서 직렬화된 모든 것에 대한 저수준 타입 표기입니다. D-Bus 타입 시그니쳐는 `(ii)`(두 개의 int32를 포함하는 구조체)처럼 생겼거나, 더 복잡하게 생겼을 수 있습니다. 예를 들어, `a{sa(usuu)}`는, 문자열로부터 uint32, string, uint32, 그리고 uint32로 이루어진 구조체의 배열에 대한 매핑을 나타냅니다(그림 20.3). 이 타입들은 데이터 형식에 관해서는 자세히 기술하지만 타입에 저장된 의미에 대한 정보는 전혀 제공하지 않습니다.

> 프로그래머들에게 의미론적 명료함을 제공하고, 언어 바인딩을 위한 타입 적용을 강화하기 위해 간단한 타입, 구조체, 맵, 열거형 그리고 플래그에 이름을 붙이기 위한 요소들이 추가되었습니다. 이 요소들은 문서와 타입 시그니쳐를 제공합니다. D-Bus 객체에 대해 객체 상속을 흉내 내기 위한 요소들도 추가되었습니다.

![D-Bus 타입 (ii)와 a{sa(usuu)}](http://aosabook.org/images/telepathy/telepathy-types-unpacked.png)

### 20.2.1. 핸들

Telepathy에서는 식별자(연락처와 대화방 이름 등)를 표현하기 위해 핸들을 사용합니다. 핸들은 부호 없는 정수로, 튜플 `(연결, 핸들 종류, 핸들)` 이 특정 연락처나 대화방에 대한 고유한 참조가 되도록 연결 관리자에 의해 할당됩니다.

식별자를 일반화시키는 방법이 통신 프로토콜마다 다르기 때문에(대소문자 구분, 자원 등), 핸들은 클라이언트가 두 식별자가 같은지 확인할 방법을 제공합니다. 클라이언트들은 두 개의 서로 다른 식별자에 대한 핸들을 요청하고, 핸들 번호가 같은 경우 해당 식별자가 같은 연락처나 대화방을 가리킨다는 것을 알 수 있습니다.

식별자의 일반화 규칙은 프로토콜마다 다르므로, 문자열로 식별자들을 구분하는 클라이언트는 잘못 구현된 것입니다. 예를 들어, XMPP 프로토콜에서 `escher@tuxedo.cat/bed`와 `escher@tuxedo.cat/litterbox`는 같은 연락처(`escher@tuxedo.cat`)의 인스턴스들이므로 같은 핸들을 가집니다. 클라이언트가 식별자나 핸들로 채널을 요청하는 것은 상관없지만, 식별자의 구분을 위해서는 핸들만을 사용해야 합니다.

### 20.2.2. Telepathy 서비스 발견

계정 관리자나 채널 배포자 등 일부 상존하는 서비스들은 Telepathy 명세에 정의되어 잘 알려진 이름을 가지고 있지만, 연결 관리자와 클라이언트의 이름들은 잘 알려져 있지 않으므로 직접 찾아야 합니다.

Telepathy에는 실행 중인 연결 관리자와 Client의 등록을 관리하는 서비스가 없습니다. 대신, D-Bus 데몬은 새로운 D-Bus 서비스가 버스에 나타났다는 신호를 발신하므로, 관심이 있다면 D-Bus 위에서 새로운 서비스에 대한 선언를 들을 수 있습니다. 클라이언트와 연결 관리자들의 이름은 Telepathy 명세에 정의된 알려진 접두어로 시작하며, 새로운 이름을 이 접두어들에 대해 비교할 수 있습니다.

이 디자인은 상태가 없다는 장점이 있습니다. Telepathy 구성요소가 시작될 때, (열려 있는 연결들을 기반으로 한 목록을 가지고 있는) 버스 데몬에게 어떤 서비스들이 실행 중인지 물어볼 수 있습니다. 예를 들어, 계정 관리자가 비정상적으로 종료되어도 실행 중인 연결들을 확인하여 다시 계정 객체들과 연관시킬 수 있습니다.

> 연결도 서비스다

> 연결 관리자는 물론, 연결 자체도 D-Bus 서비스로서 선언됩니다. 이것은 이론적으로 연결 관리자가 각 연결을 개별 프로세스로 포크할 수 있게 해주지만, 아직 이런 식으로 구현된 연결 관리자는 존재하지 않습니다. 좀 더 실용적인 관점에서 보면, 이것은 D-Bus 데몬에 이름이 `ofdT.Connection`으로 시작하는 서비스들을 조회하여 실행 중인 모든 연결을 발견하는 것을 가능하게 합니다.

> 채널 배포자 역시 Telepathy 클라이언트들을 발견하기 위해 이 방법을 사용합니다. Telepathy 클라이언트들은 `ofdT.Client.Logger`처럼 `ofdT.Client`로 시작합니다.

### 20.2.3. D-Bus 트래픽 줄이기

초기 Telepathy 명세는 과다한 D-Bus 트래픽을 발생시켰습니다. 많은 소비자가 원하는 정보를 요청하기 위해 필요한 메서드 콜 때문이었습니다. 이후 버전의 Telepathy에서는 몇 가지 최적화를 통해 이 문제를 해결하였습니다.

개별 메서드 호출은 D-Bus 속성으로 대체되었습니다. 기존 명세에선 `GetInterfaces`, `GetChannelType` 등 각 객체 속성을 위한 메서드들이 있었고 각각의 호출 오버헤드를 가졌습니다. 이후 D-Bus 속성을 사용함으로써 표준 `GetAll` 메서드로 모든 속성을 한 번에 가져올 수 있게 되었습니다.

채널 타입, 인터페이스, 연결되어 있는 대상, 요청자 등 많은 채널 속성들은 채널이 살아 있는 동안 바뀌지 않습니다. 예를 들어 파일 전송 채널의 불변 속성에는 파일 크기와 컨텐츠 타입 등이 있습니다.

불변 속성에 대한 해쉬 테이블을 포함하는, 채널의 생성을 알리기 위한 새로운 신호가 추가되었습니다. 이 신호는 클라이언트가 각자 정보를 요청할 필요 없이, 채널 생성자 프록시에 직접 전달될 수 있습니다(20.4장을 참고하세요).

사용자 아바타는 버스에서 바이트 배열의 형태로 전송됩니다. 이미 Telepathy에서는 클라이언트들에게 새로운 아바타가 필요함을 알리고, 불필요한 아바타를 받는 비용을 줄일 수 있도록 아바타를 토큰으로 구분하고 있었지만, 클라이언트들은 아바타를 받아오기 위해 `RequestAvatar` 메서드를 통해 아바타를 각자 요청해야 했습니다. 따라서 연결 관리자가 특정 연락처가 아바타를 갱신하였다는 신호를 보내면, 아바타를 요청하는 다수의 개별 요청이 일어났었고, 같은 아바타가 버스를 통해 여러 번 전송돼야 했습니다.

이 문제는 아바타를 반환하지 않는(아무것도 반환하지 않는) 새로운 메서드를 추가함으로써 해결되었습니다. 대신 이 메서드는 아바타를 요청 큐에 넣습니다. 네트워크로부터 아바타를 가져오면 `AvatarRetrieved` 신호가 발생하며, 관심 있는 모든 클라이언트가 신호를 들을 수 있습니다. 이것은 아바타가 버스 위로 한 번만 전송되면 된다는 것을 의미합니다. 클라이언트의 요청이 큐에 들어간 이상, 이후 클라이언트 요청들은 `AvatarRetrieved` 신호의 송출 이전엔 모두 무시할 수 있습니다.

많은 수의 연락처를 불러와야 할 때(연락처 목록을 불러올 때)마다 별명, 아바타, 기능, 그룹들과, 위치, 주소, 전화번호 등을 포함할 수도 있는 상당한 양의 정보가 요청되어야 합니다. 이전 Telepathy 버전에서는 정보 그룹마다 메서드 호출을 해야 했고(`GetAliases` 등 대부분의 API들은 이미 연락처 목록을 요구했습니다), 이 작업은 여섯 개 이상의 메서드 호출을 필요로 하였습니다.

이 문제를 해결해기 위해 Contacts 인터페이스가 도입되어, 여러 인터페이스로부터의 정보를 한 번의 메서드 호출로 가져올 수 있게 되었습니다. Telepathy 명세는, `GetContactAttribute` 메서드가 반환하는, 이름공간을 가진 Contact 속성들을 포함하도록 확장되었으며, 이로 인해 연락처 정보를 가져오기 위해 사용되었던 메서드 콜은 더 이상 사용되지 않게 되었습니다. 클라이언트가 `GetContactAttributes` 메서드를, 연락처와 관심 있는 인터페이스의 목록과 함께 호출하면, 연락처의 속성과 값에 대한 매핑의 목록을 돌려받게 됩니다.

코드를 보면 좀 더 명확해집니다. 다음과 같이 생긴 요청이 있으면,

~~~
connection[CONNECTION_INTERFACE_CONTACTS].GetContactAttributes(
  [ 1, 2, 3 ], # contact handles
  [ "ofdT.Connection.Interface.Aliasing",
    "ofdT.Connection.Interface.Avatars",
    "ofdT.Connection.Interface.ContactGroups",
    "ofdT.Connection.Interface.Location"
  ],
  False # 이 연락처들에 대한 레퍼런스를 가지고 있지 말라
)
~~~

이렇게 생긴 응답이 있을 수 있습니다:

~~~
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
~~~

## 20.3. 연결, 채널 그리고 클라이언트

### 20.3.1. 연결

연결은 연결 관리자가 하나의 프로토콜/계정 당 하나의 연결을 만듭니다. 예를 들어, XMPP 계정 `escher@tuxedo.cat`과 `cami@egg.cat`에 연결하는 것은 D-Bus 객체로 표현되는 두 개의 연결을 만들게 됩니다. 연결은 주로, 현재 활성화된 계정에 대해, 계정 관리자에 의해 구성됩니다.

연결은 연결 상태를 관리, 관찰하고, 채널을 요청하기 위한 몇 가지 필수적인 기능을 제공하며, 프로토콜의 기능에 따라 선택적인 기능들을 제공하기도 합니다. 이러한 기능들은 선택적인 (이전 장에서 다뤄졌던 것처럼) D-Bus 인터페이스로 제공되며, 연결의 `Interfaces` 속성에서 확인할 수 있습니다.

연결들은 주로 해당하는 계정의 속성을 사용하여 만들어진 계정 관리자에 의해 관리됩니다. 계정 관리자는 각 계정에 대한 사용자의 상태를 각 연결에 동기화시키고, 주어진 계정에 대한 연결 경로를 제공하기도 합니다.

### 20.3.2. 채널

채널은 통신이 이루어지는 체계입니다. 채널은 주로 인스턴트 메신저 대화, 음성, 영상통화나 파일 전송이지만, 서버 자체와의 상태 유지 통신(대화방이나 연락처 검색 등)을 제공할 수도 있습니다. 각 채널은 D-Bus 객체로 표현됩니다.

체널은 주로 둘 이상의 사용자들 사이에서 이루어지며, 그중 하나는 자신입니다. 채널은 주로 대상 식별자를 가지고 있으며, 이것은 1:1 통신일 경우엔 다른 연락처이거나, 다중 사용자 통신일 경우엔(대화방 등) 방 식별자입니다. 다중 사용자 채널은 `Group` 인터페이스를 제공하며, 이를 통해 현재 채널에 있는 연락처들을 알 수 있습니다.

채널은 연결에 속하며, 주로 채널 배포자를 통해 연결 관리자로부터 요청이 들어오거나, 네트워크 이벤트(걸려오는 대화 등)에 대한 응답으로써, 연결에 의해 만들어지며, 이후 배포을 위해 채널 배포자로 전달됩니다.

채널의 타입은 `ChannelType` 속성에 정의되어 있습니다. 해당 채널 타입에 필요한 핵심 기능, 메서드, 속성, 신호(문자 메시지를 송수신하는 등)들은 `Channel.Type.Text`처럼 적절한 `Channel.Type` D-Bus 인터페이스에 정의되어 있습니다. 어떤 채널 타입들은 선택적인 추가 기능(암호화 등)을 구현할 수 있으며, 채널의 `Interfaces` 속성에 추가적인 인터페이스로 정의되어 있습니다. 표 20.1에는 다중 사용자 대화방에 연결하는 텍스트 채널이 가질 수 있는 인터페이스의 예시를 보여줍니다.

속성 | 목적
- | -
`odfT.Channel` | 모든 채널에 공통적인 기능
`odfT.Channel.Type.Text` | 채널 타입(텍스트 채널에 공통적인 기능들을 포함)
`odfT.Channel.Interface.Messages` | 서식 있는 텍스트 메시징
`odfT.Channel.Interface.Group` | 이 채널의 구성원을 나열, 추적, 초대, 승인
`odfT.Channel.Interface.Room` | 제목 등 대화방의 속성을 읽고 쓰기

표 20.1: 예시 텍스트 채널

> 연락처 목록 채널: 실수

> 초기 Telepathy 명세에선 연락처 목록을 채널의 일종으로 정의했었습니다. 각 연결에서 요청할 수 있는, 서버에서 지정하는 여러 연락처 목록들(구독한 사용자, 발행 대상 사용자, 차단된 사용자)이 있었으며, 목록의 구성원들은 다중 사용자 채팅과 같이 Group 인터페이스를 통해 발견되었습니다.

> 기존 방식에서의 채널 생성은, 일부 프로토콜에서는 어느 정도의 시간이 걸리는 연락처 목록 가져오기를 한 다음에야 채널이 생성될 수 있었습니다. 클라이언트는 원하면 어느 때나 채널을 요청하고 준비되면 받을 수 있지만, 연락처가 많은 사용자에게 이 요청은 지나치게 긴 시간이 걸려 종종 자동으로 중단됩니다. 클라이언트의 구독/발행/차단 상태를 결정짓기 위해서는 세 가지 채널을 확인해야 했습니다.

> 연락처 그룹(친구 그룹 등) 역시 그룹당 하나의 채널의 형태로 노출되어 있었습니다. 이러한 구조는 클라이언트 개발자들이 다루기 매우 까다로운 것으로 판명되었습니다. 연락처가 속해 있는 그룹들의 목록을 가져오는 등의 작업을 하려면 클라이언트 측에서 매우 많은 양의 코드를 작성해야 합니다. 게다가 채널을 통해서만 정보를 받아올 수 있기 때문에 연락처의 그룹이나 구독 상태를 Contacts 인터페이스를 통해 발행할 수 없었습니다. 

> 이후 두 채널 타입은 모두 클라이언트 개발자에게 유용한 연락처 목록 정보를 노출하는, (enum 타입의) 연락처의 구독 상태, 속해 있는 그룹, 그리고 그룹에 있는 연락처들을 포함하는, 연결 자체의 인터페이스로 교체되었습니다. 시그널은 연락처 목록이 준비되었는지 여부를 알려줍니다.

### 20.3.3. 채널과 채널 속성의 요청, 그리고 배포

채널은 채널이 갖기 원하는 속성들의 매핑과 함께 요청될 수 있습니다. 일반적으로 채널 요청은 채널 타입, 대상 핸들 타입(연락처 또는 대화방)과 대상을 포함합니다. 하지만, 채널 요청은 추가적인 정보를 포함할 수도 있습니다. 파일 전송엔 파일 이름이나 파일 크기, 전화엔 초기 음성이나 영상, 전화 회의엔 합칠 기존의 채널, 연락처 검색엔 사용할 연락처 서버 등이 있습니다.

채널 요청의 속성들은 Telepathy 인터페이스 명세에 정의되어 있는 속성들로, ChannelType 속성(표 20.2) 같은 것들입니다. 이 속성들은 인터페이스의 이름공간에 의해 자격을 갖춥니다. 채널 요청에 포함될 수 있는 속성들은 그 사실이 Telepathy 명세에 정의되어 있습니다.

속성 | 값
- | -
`ofdT.Channel.ChannelType` | `ofdT.Channel.Type.Text`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact`
`ofdT.Channel.TargetID` | `escher@tuxedo.cat`

표 20.2: 채널 요청의 예시

좀 더 복잡한, 파일 전송 채널을 요청하는 예시가 표 20.3에 있습니다. 요청된 속성들이 소속된 인터페이스에 대해 적합하다는 것을 확인할 수 있습니다. (간략하게 파악할 수 있도록 필요한 속성들의 일부만 표시하였습니다).
좀 더 복잡한, 파일 전송 채널을 요청하는 예시가 표 20.3에 있습니다. 요청된 속성들이 소속된 인터페이스에 대해 적합하다는 것을 확인할 수 있습니다. (간략하게 파악할 수 있도록 필요한 속성들의 일부만 표시하였습니다).

속성 | 값
- | -
`ofdT.Channel.ChannelType` | `ofdT.Channel.Type.FileTransfer`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact`
`ofdT.Channel.TargetID` | `escher@tuxedo.cat`
`ofdT.Channel.Type.FileTransfer.Filename` | `meow.jpg`
`ofdT.Channel.Type.FileTransfer.ContentType` | `image/jpeg`

표 20.3: 파일 전송 채널 요청

채널들은 생성되거나 확보될 수 있습니다. 채널을 확보한다는 것은 채널이 존재하지 않을 시에만 생성한다는 뜻입니다. 채널 생성을 요청하는 것은 완전히 새로운 별개의 채널을 생성하거나, 해당 채널의 사본이 존재할 수 없을 경우 오류를 냅니다. 보통 텍스트 채널과 통화를 확보하며(보통 한 사람당 하나의 대화만을 원할 뿐더러, 많은 프로토콜이 같은 연락처와의 다중 개별 대화를 지원하지 않습니다), 파일 전송 그리고 상태가 있는 채널을 생성합니다.

새롭게 생성된 채널들은 (요청되었거나 아니거나) 연결로부터의 신호로 선언됩니다. 이 신호은 채널의 불변 속성들의 매핑을 포함합니다. 이 속성들은 채널이 존재하는 동안 불변성이 보장되어 있습니다. 변하지 않을 것이라고 간주되는 속성들은 Telepathy의 명세에 표시되어 있으나, 보통 채널의 타입, 타켓 핸들 타입, 타겟, 창시자(채널을 만든 사람), 그리고 인터페이스들을 포함합니다. 물론 채널의 상태 같은 속성들은 포함되지 않습니다.

> 옛 채널 요청 방식

> 기존의 채널들은 타입, 핸들 타입 그리고 대상 핸들로 요청되었습니다. 하지만 모든 채널들이 타겟을 갖는 것은 아니고(연락처 검색 채널 등), 일부 채널들은 초기 채널 요청에 추가적인 정보를 포함해야 했기 때문에(파일 전송, 음성 메시지 요청, SMS 전송 채널 등) 충분히 유연하지 않았습니다.

> 또, 채널을 요청할 때 두 개의 서로 다른 동작(고유함이 보장된 채널을 생성하거나, 단순히 채널이 존재하는지에 대한 보장만 하거나)이 일어날 수 있음이 발견되었으며, 이 전까지는 연결 객체가 어떤 동작이 일어날지 정해야 했습니다. 따라서 기존의 방식은 새롭고, 더 유연하고, 더 명시적인 방식으로 교체되었습니다.

채널을 확보하거나 생성할 때 채널의 불변 속성들은 반환하면 채널에 대한 프락시 객체의 생성을 훨씬 빠르게 만듭니다. 이제 불변 속성들을 확보하기 위한 요청을 따로 보낼 필요가 없습니다. 표 20.4의 매핑은 (표 20.3의 채널 요청을 사용하여) 텍스트 채널을 요청할 때 포함될 수 있는 불변 속성들을 보여줍니다. 일부 속성들(TargetHandle과 InitiatorHandle 등)은 간결한 설명을 위해 생략했습니다.

속성 | 값
- | -
`ofdT.Channel.ChannelType` | `Channel.Type.Text`
`ofdT.Channel.Interfaces` | `{[} Channel.Interface.Messages`, `Channel.Interface.Destroyable`, `Channel.Interface.ChatState {]}`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact`
`ofdT.Channel.TargetID` | `escher@tuxedo.cat`
`ofdT.Channel.InitiatorID` | `danielle.madeley@collabora.co.uk`
`ofdT.Channel.Requested` | `True`
`ofdT.Channel.Interface.Messages.SupportedContentTypes` | `{[} text/html, text/plain {]}`

표 20.4: 새로운 채널이 반환한 불변 속성들의 예시

요청하는 프로그램은 주로 채널 배포자에 채널 요청을 보냅니다. 이때 요청을 위한 계정, 채널 요청 그리고 선택적으로 원하는 핸들러 이름(프로그램이 채널을 직접 다룰 때 유용합니다)을 함께 보냅니다. 연결 객체 대신 계정 이름을 넘겨주기 때문에 필요할 경우 채널 배포자가 계정 관리자에게 계정을 접속시킬 것을 요청할 수 있습니다.

요청이 완료되면, 채널 배포자는 채널을 기명 Handler에 전달하거나 적절한 Handler(Handler와 다른 클라이언트에 대한 논의는 아래에서 다시 얘기합니다)를 찾습니다. 원하는 Handler의 이름을 선택사항으로 만든 것은, 초기 요청 이후 채널과의 통신이 필요 없는 프로그램들이, 채널을 요청한 후 나머지는 다른 프로그램이 처리할 수 있게 하기 위함입니다(이메일 클라이언트에서 텍스트 채팅을 시작하는 등).

![http://aosabook.org/images/telepathy/dispatching-model.png](채널 요청과 배포)

요청하는 프로그램은 채널 배포자에 채널 요청을 보내고, 채널 요청은 적절한 연결에 전달됩니다. 연결은 NewChannels 신호를 발신하고, 이 신호는 다시 해당 채널을 처리할 적절한 클라이언트를 찾는 채널 배포자에 의해 수집됩니다. 요청하지 않은 들어오는 채널들도 비슷한 방식으로 배포됩니다. 단지 프로그램으로부터의 초기 요청이 없을 뿐, 역시 연결로부터의 시그널이 채널 배포자에 의해 수집됩니다.

### 20.3.4. 클라이언트

클라이언트들은 수신 및 발신 채널들을 처리하거나 관찰합니다. 채널 배포자에 등록된 어떠한 것이든 클라이언트가 될 수 있습니다. Telepathy에는 세 종류의 클라이언트가 있습니다(개발자가 원할 경우 하나의 클라이언트는 이 종류들 중 두 개, 혹은 세 개 모두가 될 수도 있습니다).

* Observer: 채널에 개입하지 않고 관찰만 합니다. Observer들은 주로 채팅과 활동(수신 및 발신 VoIP 통화 등)을 기록하기 위해 사용됩니다.
* Approver: 사용자들이 수신 채널을 허용하거나 차단할 수 있는 기회를 주는 역할을 합니다.
* Handler: 문자 메시지들을 승인하거나 보내기, 파일을 보내거나 받기 등 채널과 실제로 상호 작용을 합니다. Handler는 사용자 인터페이스와 주로 연관됩니다.

클라이언트들은 `Client.Observer`, `Client.Approver`, 그리고 `Client` 총 세 개까지의 인터페이스에 D-Bus 서비스를 제공할 수 있습니다. 각 인터페이스는 채널 배포자가 클라이언트에게 관찰, 승인, 혹은 처리할 채널에 대해 알려 주기 위해 호출할 수 있는 메서드를 제공합니다. 

채널 배포자는 채널을 클라이언트 그룹에 순차적으로 배포합니다. 먼저, 채널은 모든 적절한 Observer들에게 배포됩니다. Observer들이 모두 반환된 이후, 채널들은 모든 적절한 Approver들에게 배포됩니다. 첫 번째 Approver가 채널을 허용하거나 차단하면, 다른 Approver들에게 그 여부가 전달되며, 최종적으로 채널이 Handler에 배포됩니다. 채널 배포가 단계별로 진행되는 이유는, Handler가 채널을 변경시키기 전에, Observer들을 구성하기 위한 시간이 필요할 수도 있기 때문입니다.

클라이언트들은 채널 필터 속성을 노출합니다. 채널 필터 속성은, 클라이언트가 관심 있는 채널의 종류를 알기 위해, 채널 배포자가 읽는 채널 필터의 목록입니다. 필터는 최소한 클라이언트가 관심 있는 채널 타입과 타겟 핸들 타입(연락처, 대화방 등)을 포함해야 하며, 더 많은 속성들을 포함할 수도 있습니다. 매칭은 채널의 불변 속성에 대한 단순 동등성 비교로 이루어집니다. 표 20.5의 필터는 모든 1:1 텍스트 채널에 매칭됩니다.

속성 | 값
- | -
`ofdT.Channel.ChannelType` | `Channel.Type.Text`
`ofdT.Channel.TargetHandleType` | `Handle_Type_Contact` (1)

표 20.5: 채널 필터의 예시

클라이언트들은 `ofdT.Client`으로 시작하는 잘 알려진 이름의 서비스들(`ofdT.Client.Empathy.Chat` 등)을 발행하기 때문에 D-Bus에서 쉽게 찾을 수 있습니다. 또, 채널 배포자가 읽을, 채널 필터를 정의하는 파일을 설치할 수도 있습니다. 이를 통해 클라이언트가 실행되고 있지 않을 경우에 채널 배포자가 클라이언트를 실행할 수 있습니다. 이러한 방식으로 클라이언트를 쉽게 찾을 수 있도록 하면 Telepathy의 다른 부분을 교체하지 않고도 사용자 인터페이스를 어느 때라도 설정하거나 수정할 수 있습니다.

> 모 아니면 도

> 모든 채널에 관심이 있다는 것을 나타내는 필터를 제공할 수도 있지만, 이런 필터는 채널 관찰에 대한 예시로서밖엔 쓸모가 없습니다. 실제 클라이언트들은 채널 타입에 종속적인 코드를 가집니다.

> 빈 채널 필터는 Handler가 어떤 채널 타입에도 관심이 없다는 것을 나타냅니다. 하지만 이름을 사용해 채널을 배포한다면 여전히 이런 핸들러에 채널을 배포할 수 있습니다. 특정 채널을 다루기 위해 생성되는 임시 Handler들이 이러한 필터를 사용합니다.

## 20.4. 언어 바인딩의 역할

Telepathy는 D-Bus API이므로, D-Bus를 지원하는 어떠한 프로그래밍 언어로도 운용될 수 있습니다. Telepathy가 언어 바인딩을 필요로 하진 않지만, 언어 바인딩은 Telepathy를 편리하게 사용할 수 있게 합니다.

언어 바인딩들은 두 개의 그룹으로 나눌 수 있습니다. 즉, Telepathy 명세, 상수, 메서드 이름 등으로부터 생성된 코드를 포함하는 저수준 바인딩, 그리고 프로그래머들이 Telepathy를 응용하여 개발할 수 있기 쉽도록 손으로 짠 고수준 바인딩이 그것입니다. 고수준 바인딩의 예로는 Glib와 Qt4 바인딩이 있습니다. 저수준 바인딩의 예로는 파이썬 바인딩과 기존의 libtelepathy C 바인딩이 있지만, GLib와 Qt4 바인딩 역시 저수준 바인딩을 포함합니다.

### 20.4.1. 비동기 프로그래밍

언어 바인딩 내에서 D-Bus를 통해 요청을 보내는 모든 메서드 호출들은, 응답이 콜백으로 주어지는 비동기적 방식으로 동작합니다. D-Bus 자체가 비동기식이므로 이런 동작 방식이 요구됩니다.

대부분의 네트워크와 사용자 인터페이스 구현처럼, D-Bus는 들어오는 신호와 메서드 반환에 대한 콜백을 발생시키기 위해 이벤트 루프를 필요로 하며, GTK+와 Qt 툴킷들이 사용하는 GLib 메인 루프와 잘 통합됩니다.

일부 D-Bus 언어 바인딩들(dbus-glib 등)은, 메서드 응답이 반환되기 전까지 메인 루프가 블록되는 가성 비동기(pseudo-synchronous) API를 제공합니다. 이 API들은 오래전 telepathy-glib API 바인딩들이 노출시켰던 것입니다. 안타깝게도 가성 비동기 API는 많은 문제점들을 내포한다는 것이 드러났으며, 결국 telepath-glib에서 제거되었습니다.

> 가성 비동기 D-Bus 호출을 사용할 수 없는 이유

> dbus-glib과 다른 D-Bus 바인딩들이 제공하는 가성 비동기 인터페이스는, 요청 후 블락하는 기법으로 작성되어 있습니다. 블락하는 도중엔 D-Bus 소켓만이 새로운 I/O를 위해 폴링되며, 해당 요청에 대한 응답이 아닌 D-Bus 메시지들은 큐에 쌓여 나중에 처리됩니다.

> 이것은 몇 가지 회피할 수 없는 중요한 문제를 만듭니다:

> * 호출자는 요청에 대한 응답을 받을 때까지 블록되며, 호출자(존재한다면, 호출자의 사용자 인터페이스 역시)는 완전히 무반응 상태가 됩니다. 요청이 네트워크를 사용한다면, 이것은 시간이 걸립니다. 즉, 피호출자에 락이 걸린 상태라면 호출이 타임아웃 될 때까지 무반응 상태를 유지하게 됩니다.
쓰레드를 만드는 것 역시 비동기식 호출의 또 다른 방식이므로 해결책이 되지 않습니다. 차라리 응답이 기존 이벤트 루프를 통해 들어오는 비동기 호출을 사용하는 것이 낫습니다.
* 메시지들의 순서가 바뀔 수 있습니다. watched-for 응답 이전에 수신된 메시지들은 큐에 쌓이게 되며, 응답을 받은 이후에 클라이언트에 전달되게 됩니다.
이는 상태 변경에 대한 시그널(객체가 소멸되는 등)이, 해당 객체에 대한 메서드 호출이 실패한 후에 (`UnknownMethod` 예외와 함께) 들어오게 되는 상황에서 문제가 됩니다. 이런 상황에서는 사용자에게 어떤 오류 메시지를 보여줘야 할지 모호하게 됩니다. 반면 시그널을 먼저 수신할 수 있다면 대기 중인 D-Bus 메서드 호출을 취소하거나 반환값을 무시하면 됩니다.
* 서로에게 가성 비동기 호출을 보내는 두 프로세스는 서로의 쿼리에 대한 응답을 기다리는 데드락을 만들 수 있습니다. 이 상황은 다른 D-Bus 서비스를 호출하는 두 프로세스가 모두 D-Bus 서비스일 경우(Telepathy 클라이언트 등)에 일어날 수 있습니다. 채널 배포자는 채널을 배포하기 위해 클라이언트의 메서드를 호출하지만, 클라이언트들 역시 새로운 채널의 생성 요청을 위해 채널 배포자의 메서드를 호출합니다(같은 과정 중 하나인, 계정 관리자를 호출할 수도 있습니다). 

C로 생성된 초기 Telepathy 바인딩들의 메서드들은 단순히 typedef 콜백 함수들을 사용하였습니다. 그리고 콜백 함수는 같은 타입 시그니쳐를 구현하기만 하면 되었습니다.

~~~
typedef void (*tp_conn_get_self_handle_reply) (
    DBusGProxy *proxy,
    guint handle,
    GError *error,
    gpointer userdata
);
~~~

이 아이디어는 단순하고 C 언어에서 잘 작동하므로 다음 세대의 바인딩들에도 포함되었습니다.

최근 몇 년 간 사람들은 GObject-Introspection이라는 GLib/GObject 기반의 API를 통해 자바스크립트나 파이썬, 그리고 C#과 유사한 언어인 Vala 같은 스크립팅 언어를 사용하기 시작했습니다. 안타깝게도, 이러한 타입의 콜백을 다른 언어로 바인딩하는 것은 매우 힘들기 때문에, 새로운 바인딩들은 해당 언어와 GLib에서 제공하는 비동기 콜백 기능을 사용하도록 설계되었습니다.

### 20.4.2. 객체의 준비성

저수준 Telepathy 바인딩 같은 간단한 D-Bus API에서는 프락시 객체를 만드는 것만으로도 D-Bus 객체의 메서드를 호출하거나 신호를 받을 수 있습니다. 단지 객체 경로와 인터페이스 이름을 주기만 하면 됩니다.

하지만 Telepathy의 고수준 API에서, 우리는 객체 프락시가 이용할 수 있는 인터페이스에 대해 알고 싶으므로, 객체 타입에 대한 공통 속성들(채널 타입, 대상, 창시자 등)을 가져올 필요가 있으며, 객체의 상태(연결 상태 등)를 판단하고 추적할 수 있어야 합니다.

따라서 모든 프락시 객체에는 준비성이라는 개념이 존재합니다. 프락시 객체에 대한 메서드 호출을 함으로써 해당 객체의 상태를 비동기적으로 받아오고, 객체를 사용할 수 있을 때 통보를 받을 수 있습니다.

모든 클라이언트가 객체의 모든 기능에 관심이 있는 것이 아니므로, 특정 객체 타입에 대한 준비성은 몇 가지 기능들로 나누어 있습니다. 각 객체는 객체에 대한 중요한 정보(객체의 Interfaces 속성과 기본 상태)를 준비하는 핵심 기능과 별도의 속성이나 상태 추적 같은 추가적인 상태에 대한 몇 가지 선택적 기능을 구현합니다. 여러 프락시에 대해 준비할 수 있는 추가적 기능의 예로는, 연락처 정보, 기능, 위치 정보, 대화 상태("아무개가 글을 쓰고 있습니다…" 등), 그리고 사용자 아바타가 있습니다.

예를 들어, 연결 객체 프락시들은 다음과 같은 기능을 가지고 있습니다.

* 인터페이스와 연결 상태를 가져오는 핵심 기능
* 요청 가능한 채널 클래스들을 가져오고 연락처 정보를 지원하는 기능
* 연결을 성사시키고, 연결되었을 때 준비 상태를 반환하는 기능

프로그래머는 관심 있는 기능들의 목록과 기능들이 준비되었을 때 호출할 콜백과 함께 객체 준비 요청을 보냅니다. 요청한 모든 기능이 준비되었을 때 콜백이 호출되며, 이미 모든 기능들이 준비되어 있으면 콜백은 즉시 호출됩니다. 

## 20.5. 견고함

견고함은 Telepathy의 핵심적인 장점입니다. Telepathy의 구성요소들은 모듈화되어 있으므로 하나의 구성요소가 고장 나도 전체 시스템이 중단되지 않습니다. 다음은 Telepathy를 견고하게 만드는 몇 가지 특징입니다.

* 계정 관리자와 채널 배포자는 상태를 회복할 수 있습니다. Mission Control(계정 관리자와 채널 배포자를 포함하는 하나의 프로세스)이 시작할 때, 사용자의 세션 버스에 등록되어 있는 서비스들의 이름을 확인합니다. 알려진 계정과 연관된 연결을 발견하면 (새로운 연결을 만드는 대신) 다시 해당 계정과 연관시키며, 실행 중인 클라이언트들이 처리하고 있는 채널의 목록을 가져옵니다.
* 클라이언트가 채널을 처리하는 도중에 사라질 경우에 채널 배포자는 클라이언트를 재실행하고 채널을 다시 등록합니다.
클라이언트가 반복적으로 중단될 경우엔 채널 배포자는 다른 클라이언트를 실행할 수 있으며, 다른 클라이언트가 없을 경우엔 (클라이언트가 처리할 수 없는 데이터에 의해 반복적으로 중단되는 것을 막기 위해) 채널을 닫습니다.
텍스트 메시지는 대기 큐에서 빠지기 전에 승인되어야 합니다. 클라이언트는 사용자가 메시지를 본 후에야(메시지 창에 포커스를 주는 등) 메시지를 승인할 수 있습니다. 이를 통해 클라이언트가 메시지를 렌더링하려는 도중에 중단된 경우에도 채널은 대기 메시지 큐에 표시하지 못한 메시지에 대한 정보를 가지고 있을 수 있습니다.
* 연결이 중단될 경우엔, 계정 관리자는 연결을 다시 만듭니다. 이 과정에서 채널의 상태는 사라지지만, 해당 프로세스의 연결에만 영향을 미칩니다. 클라이언트들은 연결들의 상태를 관찰할 수 있으며, 연락처 목록과, 다른 상태 없는 채널들에 대한 정보 등을 다시 요청하기만 하면 됩니다.

## 20.6. Telepathy 확장하기: 사이드카

Telepathy 명세는 통신 프로토콜이 노출하는 폭넓은 범위의 기능을 다루려 하지만, 어떤 프로토콜들은 프로토콜 자체가 확장될 수 있습니다[^4]. Telepathy 개발자들은 Telepathy 명세를 확장하지 않고도 사용자의 Telepathy 연결을 확장할 수 있게 하고 싶었습니다. 이는 사이드카를 통해 가능합니다.

사이드카는 일반적으로 연결 관리자의 플러그인에 의해 구현됩니다. 클라이언트들은 주어진 D-Bus 인터페이스를 구현하는 사이드카를 요청하는 메서드를 호출합니다. 예를 들어, 어떤 사람의 XEP-0016 사생활 목록 구현체는 `com.example.PrivacyLists`라는 인터페이스를 구현할 수 있습니다. 이 메서드는 (추가적으로 다른 인터페이스를 구현할 수도 있는) 해당 인터페이스를 구현하는 플러그인이 제공하는 D-Bus 객체를 반환합니다. 이 객체는 메인 연결 객체와 공존하게 됩니다(따라서 오토바이의 사이드카라는 이름을 가지게 되었습니다).

> 사이드카의 역사

> 초창기 Telepathy 시절에, 어린이 한 명당 한 대의 노트북(OLPC, One Laptop Per Child) 프로젝트는 기기 간 정보를 공유하기 위해 맞춤형 XMPP 확장(XEP)을 지원할 필요가 있었습니다. 이 확장들은 Telepathy-Gabble(XMPP 연결 매니저)에 직접, 문서화되지 않은 인터페이스로서 연결 객체에 추가되었습니다. 결과적으로 다른 통신 프로토콜과 대응되는 것이 없는 특정 XEP에 대한 지원을 필요로 하는 개발자들이 많아지며, 플러그인이 사용할 수 있는 일반화된 인터페이스의 필요성이 인정되었습니다.

## 20.7. 연결 관리자 내부 개요

대부분의 연결 관리자들은 C/GLib 언어 바인딩을 사용해 작성되었으며, 연결 관리자를 쉽게 작성할 수 있도록 몇 가지 고수준 기반 클래스들이 개발되었습니다. 위에서 논의되었던 것처럼, D-Bus 객체들은 D-Bus 인터페이스에 매핑되는 몇 가지 소프트웨어 인터페이스를 구현하는 소프트웨어 객체로부터 발행됩니다. Telepathy-GLib은 연결 관리자, 연결 그리고 연결 객체를 구현하기 위한 기반 객체와, BaseConnection이 채널 객체를 초기화, 관리 그리고 버스에 발행하기 위해 사용하는 팩토리인 채널 관리자를 구현하기 위한 인터페이스를 제공합니다.

바인딩은 믹스인을 제공합니다. 믹스인은 추가적인 기능과, 명세 API의 새로운 버전이나 더 이상 권장되지 않는 API 버전의 대한 하위 호환성을 하나의 체계를 통해 제공하는 추상화를 클래스에 더할 수 있습니다. 가장 일반적으로 사용되는 믹스인은 오브젝트에 D-Bus 속성 인터페이스를 추가하는 믹스인입니다. `ofdT.Connection.Interface.Contacts`와 `ofdT.Channel.Interface.Group` 인터페이스를 구현하는 믹스인과, 예전과 현재의 사용자 상태를 확인하는 인터페이스, 그리고 텍스트 메시지 인터페이스를 하나의 메서드 집합을 통해 구현할 수 있게 하는 믹스인도 있습니다.

![연결 관리자 설계 예시](http://aosabook.org/images/telepathy/cm.png)

> 믹스인을 통해 API 설계 실수 해결하기

> 믹스인이 Telepathy 명세의 실수를 해결하기 위해 사용된 곳 중 하나는 `TpPresenceMixin`입니다. Telepathy에 의해 노출되던 기존 인터페이스(`odfT.Connection.Interface.Presence`)는 연결과 클라이언트들 모두에게 매우 복잡하고, 구현하기 힘들며, 대부분의 통신 프로토콜에는 존재하지 않거나 거의 사용되지 않는 기능들을 노출했었습니다. 이 인터페이스는 사용자들이 실제로 필요로 하는 기능만을 노출하고, 연결 관리자에서 실제로 구현된 훨씬 간단한 인터페이스(`odfT.Connection.Interface.SimplePresence`)로 교체되었습니다.

> 사용자의 상태를 확인하는 믹스인은 옛날 클라이언트들이 계속 동작할 수 있도록, 연결을 기반으로 두 인터페이스 모두 구현하지만, 단순한 인터페이스 쪽의 기능만큼만 구현합니다.

## 20.8. 얻은 교훈

Telepathy는 D-Bus를 기반으로 한 유연하고 모듈화된 API를 만든 훌륭한 예시입니다. D-Bus를 기반으로, 중앙 관리 데몬 없이, 구성요소들이 개별적으로, 다른 구성 요소들의 데이터 손실 없이 재 시작될 수 있는, 분산된 유연한 프레임워크를 개발할 수 있다는 것을 보여줍니다. 또, Telepathy는 버스에 전송하는 트래픽을 최소화하여 D-Bus를 효율적이고 효과적으로 사용할 수 있는 방법도 보여줍니다.

Telepathy는 D-Bus의 사용 방식을 계속 반복해 개션하며 개발되었습니다. 그 과정에서 실수도 있었지만, 교훈도 얻었습니다. 다음은 우리가 Telepathy를 설계하며 얻은 몇 가지 중요한 교훈입니다.

* _D-Bus 속성을 사용합니다. 정보를 가져오기 위해 수십 개의 작은 D-Bus 메서드를 호출하지 않아도 됩니다._ 모든 메서드 호출에는 왕복 비용이 있습니다. 많은 개별 호출(`GetHandle`, `GetChannelType`, `GetInterfaces` 등)을 하는 것보다는, D-Bus 속성을 사용하여 하나의 `GetAll` 호출을 통해 정보를 반환하는 것이 낫습니다.
* _새로운 객체를 선언할 땐 최대한 많은 정보를 제공합니다._ 클라이언트가 새로운 객체의 존재를 발견하였을 때 가장 먼저 하는 일은, 해당 객체가 필요하긴 한지 알아내기 위해 해당 객체에 대한 모든 속성을 요청하는 것입니다. 객체의 불변 속성을 객체 선언 시그널에 포함시킴으로서, 대부분의 클라이언트는 메서드 호출을 하지 않고서도 객체가 필요한지 판단할 수 있습니다. 또, 객체가 필요하다고 판단될 경우에도 불변 속성에 대한 요청을 보낼 필요가 없어집니다.
* _Contacts 인터페이스는 여러 인터페이스로부터의 정보를 한번에 가져올 수 있습니다._ 연락처에 대한 정보를 가져오기 위해 `GetAll`을 여러 번 호출하는 대신, Contacts 인터페이스에 모든 정보에 대한 요청을 보내 D-Bus로의 왕복 요청 갯수를 줄일 수 있습니다.
* _애매한 추상화는 사용하지 않습니다._ 연락처 목록과 연락처 그룹을 Group 인터페이스를 구현하는 채널로 노출시키는 것이 기존의 추상화를 사용했기 때문에 처음에는 좋은 아이디어 같아 보였습니다. 하지만 이 결정은 클라이언트 구현을 어렵게 만들었으며, 결국엔 적절하지 않았습니다.
* _API가 미래의 요구사항을 충족시킬 수 있도록 보장합니다._ 기존의 채널 요청 API는 단순한 채널 요청만 보낼 수 있게 하는 등, 유연하지 못했습니다. 이런 방식은 더 많은 정보를 필요로 하는 채널에 요청을 보낼 때 우리의 요구사항에 맞출 수 없었습니다. 이 API는 결국 훨씬 더 유연한 새로운 API로 교체되어야 했습니다.

## 각주

[^1]: [http://telepathy.freedesktop.org/](http://telepathy.freedesktop.org/) 또는 [http://telepathy.freedesktop.org/doc/book/](http://telepathy.freedesktop.org/doc/book/) 의 개발자 매뉴얼 참조.
[^2]: [http://telepathy.freedesktop.org/spec/](http://telepathy.freedesktop.org/spec/)
[^3]: 여기서부터 `/org/freedesktop/Telepathy/`와 `org.freedesktop.Telepathy`는 공간 절약을 위해 `ofdT`로 줄여 쓰겠습니다.
[^4]: Extensible Messaging and Presence Protocol (XMPP) 등.
