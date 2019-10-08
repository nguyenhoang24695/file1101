README: This file contains very important information in Japanese, English and Chinese. (in the UTF-8 format)

SoftEther VPN に関する重要事項説明書

本ソフトウェアの VPN 通信機能はかつてないほど極めて強力であり、正しい使い方によりお客様は大きな利便性と利益を手にすることができます。しかし、誤った使い方を行うと不利益が発生する危険もあります。そのような危険を避けるため、本ソフトウェアのご使用に際してお客様が事前に説明を受けるべき事項を以下に記載いたします。この内容は大変重要ですから、十分理解されるようお願いいたします。また、ダイナミック DNS、NAT トラバーサルまたは VPN Azure 機能をご使用いただく前には下記の 3.5 節の注意書きをよくお読みください。この 3 つの機能はインターネット経由で提供される無償の無保証の学術実験サービスであり、障害の発生が許されないような業務において使用することは想定されておりません。


1. VPN 通信について
1.1. SoftEther VPN プロトコルについて
SoftEther VPN は VPN 通信を行うことができます。伝統的な VPN プロトコルとは異なり、SoftEther VPN には新たに設計された「SoftEther VPN プロトコル (SE-VPN プロトコル) 」が搭載されています。SE-VPN プロトコルは任意のパケットを HTTPS (HTTP over SSL) パケットにカプセル化して送受信します。これにより、既存のファイアウォールがネットワーク管理者によって通常の VPN プロトコルを通過しないように設定されている場合であっても、SE-VPN プロトコルは大抵の場合は通過します。SE-VPN プロトコルは TLS 1.0 (RFC 5246) および HTTPS (RFC 2818) に準拠するように実装されていますが、一部非準拠の動作を行う場合もあります。もしあなたがネットワーク管理者であり、ファイアウォールで SE-VPN プロトコルの通信を遮断したいと希望される場合は、ファイアウォールにホワイトリストルールを適用することにより、境界上を流れるすべての無許可の TCP および UDP パケットを遮断し、一部許可した Web サイトやサーバー等との間の通信のみ許可するように設定することでその希望を実現できます。

1.2. NAT トラバーサル機能について
従来の VPN システムの場合、NAT やファイアウォールの内側に VPN サーバーを設置する場合はネットワーク管理者に依頼して NAT やファイアウォールにおいて「ポート開放」や「ポート転送」といった設定を行ってもらう必要があります。しかし、ネットワーク管理者にそのような手間をかけずに社内の自分のコンピュータに VPN サーバーをインストールし社外から接続したいという需要に応えるため、SoftEther VPN には強力な「NAT トラバーサル機能」が搭載されています。NAT トラバーサル機能はデフォルトで有効になっています。NAT トラバーサル機能が有効に設定されている SoftEther VPN Server は、たとえ NAT やファイアウォールの内側であっても、特別な設定なしにインターネット側から VPN 接続を受付けることができます。NAT トラバーサル機能をサーバー側で無効にするには、SoftEther VPN Server の設定ファイルの「DisableNatTraversal」項目の値を「true」に変更してください。クライアント側で無効にするには、接続先の VPN サーバーのホスト名の後に「/tcp」というサフィックスを追加してください。

1.3. ダイナミック DNS 機能について
従来の VPN システムの場合、VPN サーバーには固定のグローバル IP アドレスを割当てる必要がありました。ソフトイーサ社はグローバル IP アドレスの枯渇に配慮するため、SoftEther VPN Server に「ダイナミック DNS 機能」を搭載しました。ダイナミック DNS 機能はデフォルトで有効になっています。ダイナミック DNS 機能は現在の SoftEther VPN Server が動作しているコンピュータのグローバル IP アドレスを、ソフトイーサ社が運用するダイナミック DNS サーバーに対して定期的に通知します。この際に、「abc.softether.net」 ( "abc" 部分は利用者が変更可能な任意のユニークな ID) という全世界から利用可能なホスト名 (FQDN) が割当てられます。ホスト名を知らされた VPN の利用者は、ホスト名を指定するだけで、現在の IP アドレスを知らなくてもいつでも VPN サーバーにアクセスできます。IP アドレスが変化した場合は、ダイナミック DNS サービスのホスト名に対応する IP アドレスが自動的に変化します。これにより、固定グローバル IP アドレスが不要になり、毎月発生する高額な ISP への通信コストを削減でき、法人利用であってもコンシューマ向けの安価な可変 IP アドレス接続が利用できるようになります。ダイナミック DNS 機能を無効にするには、SoftEther VPN Server の設定ファイルの「DDnsClient」ディレクティブ内の「Disabled」項目の値を「true」に変更してください。中華人民共和国でご利用される場合の注意: DNS サフィックスは中華人民共和国内で利用する場合は「sedns.cn」というドメイン名に置換されます。sedns.cn ドメインは中国企業 (北京大游索易有限公司) が運営・管理しているサービスです。

1.4. VPN over ICMP 機能および VPN over DNS 機能について
SoftEther VPN Client / Bridge が SoftEther VPN Server との間で VPN 通信を行おうとする場合、TCP と UDP の両方のプロトコルが通信できない場合のために、VPN を「ICMP」 (いわゆる Ping) および「DNS」パケットにカプセル化して通信する機能が実装されています。この機能により、ネットワーク経路上のルータやファイアウォールなどが TCP や UDP の通信を遮断してしまう場合でも、ICMP または DNS の通信が可能であれば VPN 接続を行うことができます。VPN over ICMP 機能および VPN over DNS 機能は、ICMP や DNS の規格にできる限り準拠するように設計されていますが、一部非準拠の動作を行う場合もあります。一部の設計不良のルータは大量の ICMP や DNS パケットが通過するとメモリオーバーフローなどを発生し、フリーズしたり再起動したりする場合があります。これは他の利用者にも悪影響を与える可能性があります。このようなリスクを避けるために VPN over ICMP 機能および VPN over DNS 機能を無効にするには、VPN 接続元の側で接続先のホスト名文字列の後に「/tcp」というサフィックスを追加してください。

1.5. VPN Azure クラウドサービスについて
SoftEther VPN Server が NAT やファイアウォールの内側にあり、何らかの理由で NAT トラバーサル機能、ダイナミック DNS 機能および VPN over ICMP/DNS 機能を利用できない場合は、VPN Azure クラウドサービスを利用できます。ソフトイーサ社はインターネット上で VPN Azure クラウドを運用しています。VPN Server は VPN Azure クラウドに一度接続すれば、それ以降は「abc.vpnazure.net」 (abc はユニークなホスト名) というホスト名が割当てられます。このホスト名は実際にはソフトイーサが運営するクラウドサーバーのグローバル IP アドレスに関連付けられています。VPN クライアントはこの VPN Azure ホストに対して接続することにより、VPN Azure は通信を折り返し中継して VPN サーバーに届けます。VPN Azure 機能はデフォルトで無効になっていますが、VPN Server 管理ツールで簡単に有効化することができます。

1.6. UDP 高速化機能について
SoftEther VPN には UDP 高速化機能が搭載されています。VPN を構築する 2 拠点間で UDP チャネルの構築が可能であることが検出された場合は、自動的に UDP による通信を行います。これにより VPN のスループットが向上します。UDP チャネルの構築の際には、直接的な UDP パケットの伝送が可能な場合はそれを使いますが、途中に NAT やファイアウォールがあることが検出された場合は代わりに「UDP ホールパンチング」を使用します。UDP ホールパンチングが使用される場合には、インターネット上のソフトイーサ社が運営する UDP ホールパンチングサーバーが利用されます。UDP 高速化機能は、VPN 接続元の側の設定でいつでも無効にすることができます。


2. VPN ソフトウェアについて
この節で述べる注意事項は、SoftEther VPN および VPN Gate 特有のものではなく、一般的なシステムソフトウェアに当てはまる事項です。VPN ソフトウェアを構成する SoftEther VPN Client, SoftEther VPN Server および SoftEther VPN Bridge ならびに VPN Gate 中継サービスは、バックグラウンドで動作するシステムサービスとしてコンピュータにインストールされます。システムサービスは、通常、ディスプレイに表示されません。また、システムを起動した際に自動的に、ユーザーによるログイン前であっても、バックグラウンドで動作を開始します。システムサービスが稼働しているかどうかを確認するためには、プロセス一覧を確認するか、お使いの OS のバックグラウンドサービス一覧 (Windows においては「サービス」、UNIX においては「デーモン」と呼称されます。) を確認してください。また、OS の有する機能を用いて、システムサービスを有効化、無効化、開始または停止することができます。システムサービスを管理するための GUI ツールは、システムサービスとの間で通信を行ないます。これらの管理 GUI ツールを終了しても、システムサービスは継続してバックグラウンドで動作し続けます。システムサービスは、CPU 時間、コンピュータの消費電力、メモリおよびディスクの容量を消費します。システムサービスは、電力を消費するため、コンピュータに係る電気料金や発熱が増加する可能性があります。さらに、コンピュータの機械部分の寿命が短くなる可能性もあります。

2.1. SoftEther VPN Client
SoftEther VPN Client を Windows で使用する場合は、仮想 LAN カードをコンピュータにインストールする必要があります。仮想 LAN カードは Windows 上で動作するカーネルモードドライバとして実装されています。当該ドライバは VeriSign 社の発行する証明書によってデジタル署名されており、Symantec 社による副署名もされています。ドライバのインストール時には本当にドライバをインストールするかどうかの確認メッセージが表示される場合があります。SoftEther VPN Client は可能な場合は自動的に当該確認メッセージに応答します。SoftEther VPN Client はインストール時に通信を最適化するため Windows の MMCSS (Multimedia Class Scheduler Service) の設定を最適化します。MMCSS の設定の最適化は後から元に戻すことができます。

2.2. SoftEther VPN Server / Bridge
SoftEther VPN Server / Bridge を Windows で使用する場合で「ローカルブリッジ機能」を使用する場合は、低レイヤ Ethernet パケット送受信ドライバをコンピュータにインストールする必要があります。当該ドライバは VeriSign 社の発行する証明書によってデジタル署名されており、Symantec 社による副署名もされています。SoftEther VPN Server / Bridge はローカルブリッジのために物理的な LAN カードの TCP/IP オフローディング機能を無効にする場合があります。Windows Vista / 2008 以降のバージョンでは、VPN Server が IPsec 機能を提供するために Windows Filter Platform (WFP) に適合したパケットフィルタドライバをカーネルモードに挿入します。このパケットフィルタドライバは IPsec 機能を有効にした場合のみロードされます。SoftEther VPN Server の IPsec 機能を有効にすると、Windows 標準の IPsec 機能は利用できなくなります。ただし、SoftEther VPN Server の IPsec 機能を無効にすると、この現象は元に戻ります。SoftEther VPN Server / Bridge はローカルブリッジ機能を使用するために OS の TCP/IP オフローディング機能を無効に設定します。

2.3. ユーザーモードでのインストール
SoftEther VPN Server および SoftEther VPN Bridge は Windows にユーザーモードでインストールすることができます。つまり、社内 PC などで Windows のシステム管理者権限を持っていない一般ユーザーであってもインストールを行えます。ユーザーモードでインストールを行うと一部の機能が制限されますが、大部分の機能は正常に動作します。これにより、たとえば社員が社内 PC に一般ユーザーとして VPN Server をインストールし、自宅から社内 LAN にアクセスすることもできます。技術的にはシステム管理者特権は一切不要ですが、だからといって企業の規則に反して勝手に VPN サーバーを構築することは好ましくない場合もあります。あなたが企業に所属する社員の場合で、企業の規則で無断のソフトウェアのインストールや外部との通信が禁止されている場合は、事前に企業の経営者またはネットワーク管理者から明示的な同意を得てからユーザーモードでのインストール作業を行ってください。ユーザーモードで VPN Server / VPN Bridge が動作している間は、Windows のタスクトレイにアイコンが表示されます。このアイコンが邪魔であると感じる場合は、ユーザーによる操作により非表示にすることもできます。ただし、この機能を悪用して他人のコンピュータに VPN Server を勝手にインストールし、スパイウェアとして利用してはなりません。そのような行為は法律に違反することになります。

2.4. キープアライブ通信
SoftEther VPN Server および SoftEther VPN Bridge ではデフォルトでインターネット回線を活性化したままにしておくためのキープアライブ通信機能が有効にされています。この機能により、インターネットに対して定期的にランダムな内容の UDP パケットを送信します。この機能は、モバイル回線やダイヤルアップ回線などが自動的に切断されてしまうことを防止するために有益です。キープアライブ通信機能はいつでも無効にできます。

2.5. アンインストール
SoftEther VPN ソフトウェアをアンインストールする場合は、プログラムファイルはすべて削除されます。ただし、プログラムファイル以外のファイル (たとえばプログラムの動作によって作成されたファイルやデータ) は削除されません。また、技術的な理由により、アンインストーラ本体の EXE ファイルおよびリソースファイルも削除されずに残る場合があります。これらのファイルが残留することはコンピュータの利用上悪影響はありませんが、お好みに応じて手動で削除することもできます。また、カーネルモードドライバも削除されない場合がありますが、次回 Windows 起動時から主要コードはメモリにロードされず無効になります。カーネルモードドライバも Windows の「sc」コマンドを用いてお好みに応じて手動で削除することができます。

2.6. セキュリティ
SoftEther VPN Server / Bridge をインストールした後は、速やかに管理者パスワードを設定してください。管理者パスワードが空白のまま放置すると、第三者が勝手に管理者モードで SoftEther VPN Server / Bridge に接続して管理者パスワードを設定したり、設定を変更したりすることができます。この注意事項は、Linux 版の SoftEther VPN Client にも適用されます。

2.7. アップデート通知機能
Windows 版の SoftEther VPN ソフトウェアには、アップデート通知機能が搭載されています。ソフトイーサ社の SoftEther Update サーバーに対して定期的に HTTP で通信を行い、最新版のソフトウェアがリリースされていないかどうかを確認します。もし最新版がリリースされている場合は、その旨を画面上に表示します。この目的を達成するために、現在のソフトウェアのバージョン、言語、固有識別子、IP アドレスおよび接続先 VPN サーバーのアドレスが SoftEther Update サーバーに対して送信されます。個人情報は一切送信されません。アップデート通知機能はデフォルトで有効になっていますが、設定画面からオフにすることもできます。オン / オフの設定は、VPN サーバー管理マネージャの場合は接続先の VPN サーバーごとに保存されます。

2.8. 仮想 NAT 機能
SoftEther VPN Server / VPN Bridge の仮想 HUB には「仮想 NAT 機能」が搭載されています。仮想 NAT 機能は、1 個の物理的な IP アドレスを、複数個の仮想的なプライベート IP アドレスを割当てられた VPN Client で共有するための機能です。仮想 NAT 機能の動作モードにはユーザーモードとカーネルモードの 2 種類があります。ユーザーモードで動作する場合、NAT の外側の物理的な IP アドレスは、VPN Server を動作させるコンピュータの OS のインターフェイスが持つ IP アドレスを共有します。これと異なり、カーネルモードで動作する場合は、VPN Server はコンピュータに装着されている物理的な Ethernet ネットワークアダプタをスキャンし、利用可能な IP アドレスを 1 個、物理的な Ethernet セグメント上の DHCP サーバーから取得しようと試みます。IP アドレスの取得に成功した場合は、その IP アドレスが仮想 NAT によって使用されます。この場合、物理的な DHCP サーバー上の IP プールに DHCP クライアントエントリが作成されます。物理的な Ethernet セグメント上のデフォルトゲートウェイおよび DNS サーバーが仮想 NAT を経由したインターネットとの間の通信のために使用されます。カーネルモードで動作する場合は、仮想 NAT は物理的な Ethernet セグメント上で 1 個の仮想 MAC アドレスを持ちます。カーネルモード NAT の動作が可能かどうかを判断するため、VPN Server は定期的にインターネットへの接続性をチェックします。接続性のチェックのためには、www.yahoo.com または www.baidu.com というホスト名への DNS クエリの応答の検査と、応答された IPv4 アドレス宛の TCP ポート 80 への接続の検査が実施されます。

2.9. カーネルモードコンポーネントの自動セットアップ
SoftEther VPN ソフトウェアが Windows にカーネルモードコンポーネントをインストールする必要があることが検出された場合、インストールを行うか否かを確認するメッセージが Windows によって表示される場合があります。この場合、SoftEther VPN ソフトウェアは自動的に無人セットアップモードに移行し、Windows に対してインストールを行う旨を応答します。これは、リモートから SoftEther VPN ソフトウェアを管理する際にリモート管理通信が切断され、デッドロックが発生してしまうことを防止するための措置です。


2.10. Windows Firewall への登録
SoftEther VPN ソフトウェアは、Windows Firewall に対して SoftEther VPN ソフトウェアを安全なプログラムとして自動的に登録します。この登録は、アンインストール後も残存する場合があります。登録を解除したい場合は、Windows のコントロールパネルを用いて手動で設定してください。

3. インターネットサービスについて
3.1. ソフトイーサ社が提供するインターネットサービスの内容
ソフトイーサ社は、「ダイナミック DNS」、「NAT トラバーサル」および「VPN Azure」サービスを無償で提供します。これらのサービスには SoftEther VPN のユーザーはソフトウェア内の実装を通じてインターネット経由でアクセスすることができます。これらのサービスは今後公開される予定のオープンソース版「SoftEther VPN」からも利用可能になる予定です。

3.2. 送信される情報とプライバシーの保護
SoftEther VPN ソフトウェアは、上記のサービスを利用するために、コンピュータの IP アドレス、ホスト名、VPN ソフトウェアのバージョン情報をソフトイーサ社の管理するクラウドサービス上に送信します。これらの情報は上記サービスを実現するために最低限必要なものです。一切の個人情報は送信されません。ソフトイーサ社はクラウドサービス上に蓄積された上記の IP アドレス等の情報を最低 90 日間ログに記録する場合があります。これはサービスの利用に技術的な問題が発生した場合の原因究明のために利用されます。ソフトイーサ社は当該ログ情報を日本国の裁判所または捜査機関による命令に従うためにこれらの機関の公務員 (日本国の公務員は日本国の法律により守秘義務を負わされています) に開示する場合があります。また、IP アドレスなどの情報は統計処理され、その統計結果は個別の具体的な IP アドレスが判別できないようにされた上で、インターネット上で研究成果として公表される場合があります。

3.3. VPN Azure を経由した通信データ
お客様が VPN Azure クラウドサービスを経由して VPN 通信を行う場合、3.2 の規定にかかわらず、お客様の実際の通信ペイロードが VPN Azure クラウドサービスを構成するサーバー上のメモリにごく短い時間蓄積される場合があります。これは VPN Azure サービスを提供するために当然に必要なことでありますが、通信内容はディスクなどの固定領域に記録されることはありません。ただし、日本国の「犯罪捜査のための通信傍受に関する法律 (平成 11 年 8 月 18 日法律第 137 号) 」が定める裁判官の令状を携行した捜査官からの要請があった場合は当該通信が日本国政府の公務員 (日本国の公務員は日本国の法律により守秘義務を負わされています) によって傍受され記録される可能性があります。この規定は、VPN Azure サービスのサーバーが物理的に日本国に存在している場合にのみ適用されます。

3.4. 電気通信事業法の適用
ソフトイーサ社は上記のサービスを日本国内で運用する場合において電気通信事業法の規定を受けるべき場合については電気通信事業法の規定に従い、総務大臣に届出または申請を行っております。

3.5. 無償で学術実験目的のサービス
ソフトイーサは「ダイナミック DNS」、「NAT トラバーサル」および「VPN Azure」を学術実験目的で研究開発し運営しています。そのため、これらのサービスはすべて無料でご利用いただけます。これらのサービスは「SoftEther VPN ソフトウェア製品」の一部ではなく、付随するものでもありません。これらのサービスは一切の保証がない状態で提供されるものです。実験の休止、中止や実験中の技術的問題の発生によってサービスが中断する場合があります。その場合は、ユーザーはサービスを利用できなくなります。ユーザーはこのようなリスクがあること、およびそのリスクをユーザー自身が負担することを承諾いただいた上でこれらのサービスをご利用ください。ソフトイーサ社はユーザーがこれらのサービスを利用した結果、または利用できなかった結果について一切の責任を負いません。仮にお客様が SoftEther VPN ソフトウェアの商用製品を購入され、SoftEther VPN ソフトウェアのライセンス料金をお客様がすでにお支払いいただいている場合であっても、当該料金にはこれらのサービスの対価は含まれていません。これらのサービスが中断したり利用不能になったりした場合であっても、SoftEther VPN ソフトウェアのライセンス料金は一切返金されず、その他の損害賠償も提供されません。

3.6. DNS プロキシ
いくつかの地域では、インターネットを利用する際、DNS クエリによる IP アドレスの取得が回線の通信不良によりしばしば誤った値を返すようです。SoftEther VPN Server, Client または Bridge を使用している場合で、本来の DNS サーバーへのアクセスができない、またはネットワーク上の途中の経路の DNS サーバーが動作不良を起こしている可能性がある場合が検出されたときは、DNS クエリはソフトイーサが運営する DNS プロキシサーバーに転送されます。DNS プロキシサーバーは本来の DNS サーバーに対してアクセスを行い、正確な IP アドレスを取得してその IP アドレスを呼出し元に返信します。


4. その他の注意事項
4.1. ネットワーク管理者による承諾の必要性
SoftEther VPN はネットワーク管理者による特別な設定を必要とせずに動作するようにパワフルな機能が実装されています。たとえば、ネットワーク管理者にファイアウォールの設定の変更を依頼しなくても VPN 通信を行うことができます。SoftEther VPN のこうした特徴は、あくまでも技術的にネットワーク管理者による手間やコスト削減するため、またはファイアウォール設定の変更に伴う設定ミスなどの危険を防止するためのものです。企業に所属する社員は、SoftEther VPN を企業の管理するネットワーク内のコンピュータにインストールまたは使用する場合にあたっては、必ず事前にネットワーク管理者の許諾を得なければなりません。もしネットワーク管理者がそのような承諾を提供しない場合は、代わりにネットワーク管理者よりもより上位の権限を持った経営者から許諾を得ることを検討してください。これらの正当な許諾がない状態で SoftEther VPN を使用することは、お客様にとって不利益な結果となる場合があります。ソフトイーサ社は SoftEther VPN の使用によってお客様に生じた一切の責任を負いません。

4.2. 各地域における法律の遵守
VPN 通信のような暗号化通信が法律で禁止されている国・地域では、SoftEther VPN を使用する場合は必ず暗号化機能をオフにして使用してください。この他、一部の国・地域では特定の方法での SoftEther VPN の利用が法律によって禁止されている場合があります。ソフトイーサ社は日本国に所在する法人ですので、他の国・地域に制定されている法令については一切関知しておりません。たとえば、SoftEther VPN の一部の機能が特定の国・地域でのみ有効な特許権を侵害している可能性もあります。ソフトイーサ社はその国・地域に関して特段の関心はありません。したがって、SoftEther VPN の機能がお客様の居住している国・地域において法的に利用可能であるかどうかは、お客様ご自身によって事前に十分検証の上ご利用ください。そもそも世界には 200 カ国近くの国が存在しており、それぞれの国における法律は互いに異なります。すべての国の法律を調査した上でそれらすべてに適合することを保証したソフトウェアをリリースすることは事実上不可能です。ソフトイーサ社は日本国の法律のみを調査し、日本国の法律下でおいて適法に利用可能なソフトウェアを提供することのみを目的に研究開発を行っております。万一お客様が SoftEther VPN の機能をお客様の居住している国・地域の領域内で利用されたことによって国家権力により法的なペナルティを科せられるなどの損害が発生した場合であっても、ソフトイーサ社は一切責任を負いません。


5. VPN Gate 学術実験プロジェクト
(この章は VPN Gate 学術実験プロジェクトに関する機能拡張プラグインが含まれているバージョンの SoftEther VPN にのみ適用されます。商用版の SoftEther VPN ソフトウェアには VPN Gate 機能拡張プラグインは含まれていませんので、この章の内容は関係ありません。)
5.1. VPN Gate 学術実験プロジェクトについて
VPN Gate 学術実験プロジェクトは、日本に所在する筑波大学大学院における学術的な研究を目的として実施されているオンラインサービスです。本研究は、グローバルな分散型公開 VPN 中継サーバーに関する知見を得ることを目的としています。詳しくは http://www.vpngate.net/ をご参照ください。

5.2. VPN Gate サービスについて
SoftEther VPN Server および SoftEther VPN Client には「VPN Gate サービス」と呼ばれるプログラムが同梱されている場合があります。ただし、VPN Gate サービスはデフォルトで無効となっています。
VPN Gate サービスは、SoftEther VPN Server または SoftEther VPN Client をインストールするコンピュータの所有者が、自らの意思に基づき、VPN Gate 学術実験に参加される場合にのみ有効にしてください。VPN Gate サービスを有効にすると、コンピュータは VPN Gate 学術実験サービスにおけるグローバルな分散型公開 VPN 中継サーバーとして動作を開始します。そして、コンピュータの IP アドレスやホスト名などの情報が筑波大学内で運用されている VPN Gate 学術実験サービスのディレクトリに登録され、公衆の閲覧に供されます。これにより、世界中にある VPN Gate Client と呼ばれるクライアントソフトウェアは当該 VPN Gate サービスが稼働している VPN サーバーコンピュータに対して VPN 接続を行うことができるようになります。VPN 接続が継続している期間中は、VPN Gate Client のコンピュータはすべての通信を VPN Gate サービスを経由してインターネットとの間で行うことができます。その際は、VPN Gate サービスを動作させているコンピュータのインターネット上におけるグローバル IP アドレスが、当該通信の発信元の IP アドレスとして使用されます。
VPN Gate サービスは、VPN Gate 学術実験サービスのディレクトリサーバーに対して、5.5 の運営者情報、ログ設定、起動時間、OS の種類、プロトコルの種類、ポート番号、回線品質情報、統計情報、VPN Gate クライアントからの接続ログ (日時、IP アドレス、バージョン番号、ID) およびソフトウェアのバージョン情報を送信します。これらの情報はディレクトリ上で公衆の閲覧に供されます。また、VPN Gate サービスは 5.9 で説明されている機能のエンコードのためのキーを VPN Gate 学術実験サービスのディレクトリサーバーから受信します。

5.3. VPN Gate サービスの動作の詳細
デフォルトで無効化されている VPN Gate サービスをユーザーの操作により有効にすると、SoftEther VPN Server 内に "VPNGATE" という名称の仮想 HUB が作成されます。SoftEter VPN Client 上において VPN Gate サービスを有効にしようとすると、まず SoftEther VPN Client 内の同一プロセス上で簡易的に動作する SoftEther VPN Server と同等のプログラムが起動し、その中で "VPNGATE" という名称の仮想 HUB が作成されます。当該仮想 HUB には "VPN" という名前のユーザーが作成され、匿名でインターネット上の誰でもが当該仮想 HUB に VPN 接続を行うことができるようになります。いったん "VPNGATE" 仮想 HUB に接続した VPN クライアントコンピュータが開始したすべての通信は "VPNGATE" 仮想 HUB を通過し、SoftEther VPN Server (または SoftEther VPN Client) が動作しているコンピュータの物理的なネットワークインターフェイスを経由してインターネットに対して伝送されます。そのため、インターネット上の宛先ホストは、あたかも当該通信が SoftEther VPN Server が動作しているコンピュータから発信されたものであるかのように識別することとなります。ただし、宛先が 192.168.0.0/255.255.0.0, 172.16.0.0/255.240.0.0 および 10.0.0.0/255.0.0.0 宛のパケットはプライベートネットワーク (たとえば社内 LAN など) で使用されているものと見なされ、"VPNGATE" 仮想 HUB を経由して伝送されることはありません。VPN Gate サービスを社内 LAN などにあるコンピュータで動作させても、VPN Gate のユーザーに対して社内 LAN 上の他のコンピュータにアクセスすることを許すことにはならないため安全です。VPN Gate サービスはまた、VPN Gate ディレクトリサーバーへのアクセスの中継も実施します。
VPN Gate サービスは、ファイアウォールや NAT などと共に良好に動作することができるようにするため、1.2 で解説されている NAT トラバーサル機能を用いて UDP ポートを開きます。また、いくつかの TCP ポートを Listen 状態とし、いくつかの TCP ポートおよび UDP ポートについて Universal Plug and Play (UPnP) プロトコルを用いて定期的にローカルのルータに対してポート開放を要求します。ルータの挙動によっては、ポートは VPN Gate サービスの停止後も開放され続ける場合がありますので、UPnP ポートを閉じたい場合は手動で閉じてください。
VPN Gate サービスはまた、www.vpngate.net のミラーサイト機能も提供します。これは、VPN Gate Web サイトにアクセスしようとするインターネット上のユーザーに対して www.vpngate.net のサイトのコピーのコンテンツを、簡易的な HTTP サーバーを経由してホストする仕組みです。簡易的な HTTP サーバー機能は VPN Gate サービスのプログラムの一部として稼働し、自分自身を www.vpngate.net のミラーサイト一覧ページに自動的に登録します。ただし、www.vpngate.net 以外のサーバーに対する中継通信はサポートしません。

5.4. VPN Gate サービスにおけるインターネットとの間の通信
VPN Gate サービスは「2.8. 仮想 NAT 機能」で説明されている機能を用いることにより、ユーザーの通信をインターネットに対してルーティングします。また、VPN Gate サービスはインターネット回線の品質を調査するため、一定時間ごとに筑波大学に設置されている Ping サーバーおよび Google 社に設置されている Public DNS Server (IP アドレス: 8.8.8.8) に対して Ping パケットを送信します。また、筑波大学に設置されている通信速度測定サーバーに対して TCP でコネクションを確立し、数十秒程度の通信を行います。これらの品質データは測定後に自動的に VPN Gate 学術実験プロジェクトの中央サーバーに伝送され保存されます。その結果は公衆の閲覧に供されます。これらの定期的な通信はネットワークに影響をできるだけ与えないようにするため最小量に調整されていますが、回線を圧迫する場合もあります。

5.5. VPN Gate サービスの運営者情報
VPN Gate 学術実験プロジェクトに参加したコンピュータ上で動作する VPN Gate サービスは、インターネット上で公衆に対してサービスを提供する分散ノードの一員となります。したがって、当該コンピュータの管理者はサーバーの運営者情報を適切に申告しなければなりません。運営者情報には、運営者氏名および不正利用等があった場合の連絡先メールアドレスを含みます。運営者情報は VPN Gate サービスの設定画面からいつでも入力することができます。入力された運営者情報は自動的に VPN Gate 学術実験プロジェクトの中央サーバーに伝送され保存されます。その結果は公衆の閲覧に供されますので、入力の際には十分注意してください。なお、入力がない場合は運営者情報としてデフォルトでコンピュータのホスト名の後に "'s owner" という文字列を付加した文字が使用されます。

5.6. VPN Gate サービスを運営する場合の法令の遵守
ユーザーが VPN Gate サービスを運営する場合、国・地域によってはそのようなサービスを運営することについて予め行政機関による許可を得るか、または行政機関に事前に届け出る必要がある規定がある場合があります。そのような規定が存在する場合は、VPN Gate サービスを有効にする前に必ず法令によって要求されている手続きを履行してください。本ソフトウェアの開発者または VPN Gate 学術実験プロジェクトの実施者は、VPN Gate サービスを稼働させたユーザーが法令において規定されている義務を履行しなかったことによって生じた法的責任または損害について一切責任を負いませんのでご注意ください。

5.7. 通信の秘密の保護
多くの国の法令において、VPN Gate サービスの運営者は、VPN Gate サービスの内部を通過した第三者の通信についてその秘密を保護することが要求されることとなりますので、ご注意ください。

5.8. パケットログ
VPN Gate サービスを経由して伝送される主要な通信パケットの重要なヘッダ部分を記録する「パケットログ」機能が VPN Gate サービスのプログラムに実装されています。パケットログは、VPN Gate サービスを経由して第三者が違法な通信を行った場合に、その事実を記録するための機能です。パケットログと VPN 接続の受付ログを参照することにより、当該通信を行った者の原 IP アドレスを特定することが可能です。このような調査などの正当な目的のためだけにパケットログを使用してください。パケットログを正当な目的以外のために閲覧したり、内容を漏洩したりすることは、5.7 の規定に反することとなります。

5.9. パケットログの自動アーカイブ機能
VPN Gate 学術実験プロジェクトは日本国憲法および法律に従って運営されています。日本国憲法や法令は、通信の秘密について非常に厳しい保護を要求しています。日本国におけるルールに従うために、VPN Gate サービスのプログラムには「自動ログファイルエンコード」機能が搭載されており、デフォルトで有効になっています。
デフォルトでは、VPN Gate サービスの現在の設定は、2 週間以上が経過したパケットログファイルを自動的にエンコードしてアーカイブするようになっています。VPN Gate サービスを経由して通信を行ったユーザーの通信の秘密を保護するため、一旦エンコードされたファイルは、VPN Gate サービスが動作しているコンピュータの管理者であっても閲覧することはできません。これにより VPN Gate サービスを利用するエンドユーザーのプライバシーが保たれます。
パケットログファイルが生成後 2 週間以上経過した後でも自動的にエンコードされないようにするためには、VPN Gate サービスの設定を変更してください。この場合は、パケットログファイルは恒久的にディスク上に平文で残ることになります。したがって、ユーザーの通信の秘密を侵害しないように十分ご注意ください。
VPN Gate サービスを経由してエンドユーザーが違法行為を行った際など、エンコードされたパケットログファイルをデコードし通信内容を復元する必要が生じた場合は、筑波大学大学院 VPN Gate 学術実験プロジェクトの運営者に連絡してください。連絡方法は http://www.vpngate.net/ に記載されています。プロジェクトの運営者は、既存の法令に従い、裁判所などの司法機関による要請およびこれに準じる要請があった場合にデコードに応じます。

5.10. 日本国の領域内で VPN Gate サービスを運営する場合の注意点
ユーザーが日本国の領域内で VPN Gate サービスを運営する場合において、その行為が電気通信役務を他人の需要に応ずるために提供する事業に該当する場合は、当該 VPN Gate サービスの提供行為は電気通信事業法 (昭和 59 年 12 月 25 日法律第 86 号) における「電気通信事業」に該当する可能性があります。ただし、そのような場合であっても、「電気通信事業参入マニュアル［追補版］」(平成 17 年 8 月 18 日発行 総務省電気通信事業部データ通信課) によれば、収益が生じない場合は電気通信事業者には該当しないこととなります。従って、収益目的において稼働させる場合を除き、VPN Gate サービスを稼働させても登録・届出が必要な「電気通信事業者」には該当しません。たとえ電気通信事業者に該当しない場合においても、電気通信事業法で規定されている「秘密の保護」の義務は生じることとなります。これらのことから、日本国の領域内で VPN Gate サービスを運営する場合においては、VPN Gate サービスの運営者は自己の管理する VPN Gate サービスを経由して行われた第三者の通信内容の秘密を漏洩してはなりません。
この節における注意事項は、日本国の領域外においては適用されません。

5.11. VPN Gate クライアント
SoftEther VPN Client に VPN Gate クライアントプラグインが含まれている場合は、ユーザーは SoftEther VPN Client を使用してインターネット上で稼働している VPN Gate サービスの一覧を取得し、いずれかの VPN Gate サービスのサーバーを指定してそのサーバーに接続することができます。
VPN Gate クライアントは起動中は常時、VPN Gate サービスのサーバーの一覧を取得するための通信をインターネット上のホストとの間で一定時間ごとに行います。そのため、通信量または通信時間に応じて課金が発生するようなインターネット接続回線を利用中の場合は十分ご注意ください。
VPN Gate クライアントを起動する際には、VPN Gate サービスを有効にするかどうかを選択する画面が表示される場合があります。VPN Gate サービスについては上記の説明を参照してください。

5.12. VPN Gate 学術実験への参加または使用前のご注意
VPN Gate 学術実験サービスは、日本国に所在する筑波大学大学院における研究プロジェクトとして運営されているサービスです。本サービスは日本国の法令にのみ準拠して運用されており、日本国以外の国・地域の法令については一切関知しておりません。
そもそも世界には 200 カ国近くの国が存在しており、それぞれの国における法律は互いに異なります。すべての国の法律を調査した上でそれらすべてに適合することを保証したソフトウェアを開発することは事実上不可能です。万一ユーザーが本サービスを特定の国・地域の領域内で利用したことによって公務員により法的なペナルティを科せられるなどの損害が発生した場合であっても、プロジェクト実施者は一切責任を負いません。
本ソフトウェアまたはサービスを使用する際には、ユーザーが適用されるすべての法令をユーザーの責任により遵守してください。本ソフトウェアまたはサービスを日本国内・国外を問わず使用された場合に発生するすべての損害と責任は、ユーザーに帰責します。本学術実験の運営者およびソフトウェアの供給者は、一切責任を負いません。
これらの注意事項に同意いただけない場合は、VPN Gate 学術実験サービスに関連する機能を使用しないでください。
VPN Gate は筑波大学大学院における学術目的の研究プロジェクトです。VPN Gate ソフトウェアはフリーウェアである SoftEther VPN およびオープンソースである UT-VPN を拡張するプラグインの形で開発されていますが、これは本研究プロジェクトにおいて開発されたものであり、ソフトイーサ株式会社によって開発されたものではありません。本研究はソフトイーサ株式会社が主宰、推進または保証するものではありません。
VPN 通信が禁止されている国・地域では VPN Gate を使用しないでください。

5.13. VPN Gate Client に組み込まれている検閲用ファイアウォールの回避のための P2P 中継機能について
2015 年 1 月以降にリリースされた VPN Gate Client には P2P 中継機能が搭載されています。この P2P 中継機能は検閲用ファイアウォールの回避の強化を目的としています。あなたの VPN Gate Client で P2P 中継機能が有効となっている場合は、P2P 中継機能は、専らあなたと同じ地域に居住する他の VPN Gate のユーザーからの VPN 接続を受け付け、当該 VPN 通信を、検閲用ファイアウォールの外側にある、自由な (検閲のない) インターネット接続環境にある他人が遠隔地に設置した VPN Gate Server に対して中継します。この中継機能においては、あなたの VPN Gate Client の P2P 中継機能に接続した VPN Gate ユーザーの VPN Gate 使用中における NAT の出口 IP アドレスはあなたのコンピュータに置き換わることはありません。なぜならば、当該中継機能は VPN トンネルを反射状に中継するものであり、VPN トンネルの最終的な終端点は当該他人が設置した VPN Gate Server となるためです。しかしながら、当該他人が設置した VPN Gate Server における VPN トンネルの接続元 IP アドレスとしては、あなたのコンピュータの IP アドレスが記録されます。また、あなたのコンピュータの P2P 中継機能を経由して行われたパケットは、5.8 に準じてあなたのコンピュータに記録されます。P2P 中継機能を有する VPN Gate Client をインストールした後に当該 P2P 中継機能が動作する状態となった場合には、5.2, 5.3, 5.4, 5.5, 5.6, 5.7, 5.8, 5.9, 5.10, 5.11 および 5.12 において VPN Gate サービス (VPN サーバー機能) を明示的に有効にした場合と同じ注意事項が適用されます。P2P 中継機能が有効な場合、あなたのコンピュータの IP アドレスおよび 5.5 で述べられているデフォルトの運営者名は、VPN Gate Project が配布する VPN Gate のサーバーリストに自動的に追加されます。5.5 で述べられている情報は、"vpn_gate_relay.config" ファイルを編集することで変更することができます。設定を変更する際には、最初に VPN Client サービスを停止する必要があります。VPN Gate Client は、あなたのコンピュータの P2P 中継機能を、あなたのコンピュータが検閲用ファイアウォールが存在する地域に存在している可能性を検出した場合に自動的に有効にします。もし P2P 中継機能を無効にしたい場合は、VPN Client の設定ファイルである "vpn_client.config" ファイル内の "DisableRelayServer" フラグを "true" に設定しなければなりません。設定を変更する際には、最初に VPN Client サービスを停止する必要があります。P2P 中継機能は、法令によって検閲用ファイアウォールの回避のための P2P 中継機能の提供が禁止されている国または地域であっても、自動的に有効になる可能性があります。そのため、法令によって検閲用ファイアウォールの回避のための P2P 中継機能の提供が禁止されている国または地域のユーザーは手動で "DisableRelayServer" フラグを変更し、P2P 中継機能を自己の責任で直ちに無効にしなければなりません。

---

THE IMPORTANT NOTICES ABOUT SOFTETHER VPN

FUNCTIONS OF VPN COMMUNICATIONS EMBEDDED ON THIS SOFTWARE ARE VERY POWERFUL THAN EVER. THIS STRONG VPN ABILITY WILL BRING YOU HUGE BENEFITS. HOWEVER, IF YOU MISUSE THIS SOFTWARE, IT MIGHT DAMAGE YOURSELF. IN ORDER TO AVOID SUCH RISKS, THIS DOCUMENT ACCOUNTS IMPORTANT NOTICES FOR CUSTOMERS WHO ARE WILLING TO USE THIS SOFTWARE. THE FOLLOWING INSTRUCTIONS ARE VERY IMPORTANT. READ AND UNDERSTAND IT CAREFULLY. ADDITIONALLY, IF YOU ARE PLANNING TO USE THE DYNAMIC DNS, THE NAT TRAVERSAL OR THE VPN AZURE FUNCTIONS, READ THE SECTION 3.5 CAREFULLY. THESE FUNCTIONS ARE FREE SERVICES PROVIDED VIA THE INTERNET, ARE NOT GUARANTEED, AND ARE NOT INTENDED TO BE USED FOR BUSINESS OR COMMERCIAL USE. DO NOT USE THESE SERVICES FOR YOUR BUSINESS OR COMMERCIAL USE.


1. VPN Communication Protocols
1.1. SoftEther VPN Protocol
SoftEther VPN can perform VPN communication. Unlike traditional VPN protocols, SoftEther VPN has an implementation of the newly-designed "SoftEther VPN Protocol (SE-VPN Protocol)" . SE-VPN protocol encapsulates any Ethernet packets into a HTTPS (HTTP over SSL) connection. Therefore SE-VPN protocol can communicate beyond firewalls even if the firewall is configured to block traditional VPN packets by network administrator. SE-VPN protocol is designed and implemented to comply TLS 1.0 (RFC 5246) and HTTPS (RFC 2818). However, it sometimes have different behavior to RFCs. If you are a network administrator and want to block SE-VPN protocols on the firewall, you can adopt a "white-list" policy on the firewall to filter any TCP or UDP packets on the border except explicitly allowed packets towards specific web sites and servers.

1.2. NAT Traversal Function
Generally, if you use traditional VPN systems you have to request a network administrator to make the NAT or firewall to "open" or "relay" specific TCP or UDP ports. However, there are demands somehow to eliminate such working costs on network administrators. In order to satisfy such demands, SoftEther VPN has the newly-implemented "NAT Traversal" function. NAT Traversal is enabled by default. A SoftEther VPN Server running on the computer behind NAT or firewall can accept VPN connections from the Internet, without any special configurations on firewalls or NATs. If you want to disable the NAT Traversal function, modify the "DisableNatTraversal" to "true" on the configuration file of SoftEther VPN Server. In order to disable it on the client-side, append "/tcp" suffix on the destination hostname.

1.3. Dynamic DNS Function
Traditional legacy VPN system requires a static global IP address on the VPN server. In consideration of shortage of global IP addresses, SoftEther Corporation implements the "Dynamic DNS Function" on SoftEther VPN Server. Dynamic DNS is enabled by default. Dynamic DNS function notify the current global IP address of the PC to the Dynamic DNS Servers which are operated by SoftEther Corporation. A globally-unique hostname (FQDN) such as "abc.softether.net" ( "abc" varies as unique per a user) will be assigned on the VPN Server. If you tell this unique hostname to a VPN user, the user can specify it as the destination VPN Sever hostname on the VPN Client and will be able to connect the VPN Server. No IP addresses are required to know beforehand. If the IP address of the VPN Server varies, the registered IP address related to the hostname of Dynamic DNS service will be changed automatically. By this mechanism, no longer need a static global IP address which costs monthly to ISPs. You can use consumer-level inexpensive Internet connection with dynamic IP address in order to operate an enterprise-level VPN system. If you want to disable Dynamic DNS, specify "true" on the "Disabled" items of the "DDnsClient" directive on the SoftEther VPN Server configuration file. * Note for residents in People's Republic of China: If your VPN Server is running on the People's Republic of China, the DNS suffix will be replaced to "sedns.cn" domain. The "sedns.cn" domain is the service possessed and operated by "Beijing Daiyuu SoftEther Technology Co., Ltd" which is a Chinese-local enterprise.

1.4. VPN over ICMP / VPN over DNS functions
If you want to make a VPN connection between SoftEther VPN Client / Bridge and SoftEther VPN Server, but if TCP and UDP packets are prohibited by the firewall, then you can encapsulates payloads into "ICMP" (as known as Ping) or "DNS" packets. This function can realize a VPN connection by using ICMP or DNS even if the firewall or router blocks every TCP or UDP connections. VPN over ICMP / VPN over DNS functions are designed to comply standard ICMP and DNS specifications as possible, however it sometimes has a behavior not to fully comply them. Therefore, few poor-quality routers may be caused a memory-overflow or something troubles when a lot of ICMP or DNS packets are passed, and such routers sometimes freezes or reboots. It might affects other users on the same network. To avoid such risks, append the suffix "/tcp" on the destination hostname which is specified on the VPN-client side to disable VPN over ICMP / DNS functions.

1.5. VPN Azure Cloud Service
If your SoftEther VPN Server is placed behind the NAT or firwall, and by some reason you cannot use NAT Traversal function, Dynamic DNS function or VPN over ICMP/DNS function, you can use VPN Azure Clouse Service. SoftEther Corporation operates VPN Azure Cloud on Internet. After the VPN Server makes a connection to the VPN Azure Cloud, the hostname "abc.vpnazure.net" ( "abc" is a unique hostname) can be specified to connect to the VPN Server via the VPN Azure Cloud. Practically, such a hostname is pointing a global IP address of one of cloud servers which are operated by SoftEther Corporation. If A VPN Client connects to such a VPN Azure host, then the VPN Azure host will relay all traffics between the VPN Client and the VPN Server. VPN Azure is disabled by default. You can activate it easily by using VPN Server Configuration Tool.

1.6. UDP Acceleration
SoftEther VPN has the UDP Acceleration Function. If a VPN consists of two sites detects that UDP channel can be established, UDP will be automatically used. By this function, throughput of UDP increases. If direct UDP channel can be established, direct UDP packets will be used. However, if there is something obstacles such as firewalls or NATs, the "UDP Hole Punching" technology will be used, instead. The "UDP Hole Punching" uses the cloud servers which SoftEther Corporation operates on Internet. UDP Acceleration can be disabled anytime by setting up so on the VPN-client side.


2. VPN Software
The notes in this section are not specific to SoftEther VPN or VPN Gate, but apply to general system software. SoftEther VPN Client, SoftEther VPN Server, SoftEther VPN Bridge, and VPN Gate Relay Service will be installed on your computer as system services. System services always run in the background. System services usually do not appear on the computer display. Then your computer system is booted, system services automatically start in the background even before you or other users log in. To check whether SoftEther-related system service is running, check the process list or the background service list of your OS (called as "Services" in Windows, or "Daemons" in UNIX.) You can activate, deactivate, start, or stop system services using the functions of the OS anytime. SoftEther-related GUI tools for managing system services communicate with these system services. After you terminate these management GUI tools, SoftEther-related system services will continue to run in the background. System services consume CPU time, computer power, memory and disk space. Because system services consume power, your electricity charges and amount of thermal of your computer increase as result. In addition, there is a possibility that the mechanical parts of the life of your computer is reduced.

2.1. SoftEther VPN Client
If you use SoftEther VPN Client on Windows, the Virtual Network Adapter device driver will be installed on Windows. The Virtual Network Adapter is implemented as a kernel-mode driver for Windows. The driver is digitally-signed by a certificate issued by VeriSign, Inc. and also sub-signed by Symantec Corporation. A message to ask you want to sure install the driver might be popped up on the screen. SoftEther VPN Client may response the message if possible. SoftEther VPN Client also optimizes the configuration of MMCSS (Multimedia Class Scheduler Service) on Windows. You can undo the optimizations of MMCSS afterwards.

2.2. SoftEther VPN Server / Bridge
If you use SoftEther VPN Server / Bridge on Windows with "Local Bridge" functions, you have to install the low-level Ethernet packet processing driver on the computer. The driver is digitally-signed by a certificate issued by VeriSign, Inc. and also sub-signed by Symantec Corporation. SoftEther VPN Server / Bridge may disable the TCP/IP offloading features on the physical network adapter for Local Bridge function. In Windows Vista / 2008 or greater version, VPN Server may inject a packet-filter driver which complies Windows Filter Platform (WPF) specification into the kernel in order to provide IPsec function. The packet-filter driver will be loaded available only if IPsec function is enabled. Once you enables IPsec function of SoftEther VPN Server, the built-in IPsec function of Windows will be disabled. After you disabled IPsec function of SoftEther VPN Server, then the built-in IPsec function of Windows will revive. In order to provide the Local Bridge function, SoftEther VPN Server / Bridge disables the TCP/IP offloading function on the operating system.

2.3. User-mode Installation
You can install SoftEther VPN Server and SoftEther VPN Bridge as "User-mode" on Windows. In other words, even if you don't have Windows system administrator's privileges, you can install SoftEther VPN as a normal user. User-mode install will disable a few functions, however other most functions work well. Therefore, for example, an employee can install SoftEther VPN Server on the computer in the office network, and he will be able to connect to the server from his home. In order to realize such a system by user-self, no system administrative privileges are required in the view-point of technical. However, breaking rules of the company to install software on the computer without authority might be regarded as an unfavorable behavior. If you are an employee and belong to the company, and the company-policy prohibits installing software or making communications towards Internet without permission, you have to obtain a permission from the network administrator or the executive officer of your company in advance to install SoftEther VPN. If you install VPN Server / Bridge as User-mode, an icon will be appeared on the Windows task-tray. If you feel that the icon disturbs you, you can hide it by your operation. However, you must not exploit this hiding function to install VPN Server on other person's computer as a spyware. Such behavior might be an offence against the criminal law.

2.4. Keep Alive Function
SoftEther VPN Server and SoftEther VPN Bridge has Keep Alive Function by default. The purpose of this function is to sustain the Internet line active. The function transmits UDP packets with a random-byte-array-payload periodically. This function is useful to avoid automatic disconnection on mobile or dial-up connections. You can disable Keep Alive Function anytime.

2.5. Uninstallation
The uninstallation process of SoftEther VPN software will delete all program files. However, non-program files (such as files and data which are generated by running of programs) ) will not be deleted. For technical reason, the exe and resource files of uninstaller might remain. Such remaining files never affects to use the computer, however you can delete it manually. Kernel-mode drivers might not be deleted, however such drivers will not be loaded after the next boot of Windows. You can use "sc" command of Windows to delete kernel-mode drivers manually.

2.6. Security
You should set the administrator's password on SoftEther VPN Server / Bridge after installation. If you neglect to do it, another person can access to SoftEther VPN Server / Bridge and can set the password without your permission. This caution might be also applied on SoftEther VPN Client for Linux.

2.7. Automatic Update Notification
SoftEther VPN software for Windows has an automatic update notification function. It accesses to the SoftEther Update server periodically to check whether or not the latest version of software is released. If the latest version is released, the notification message will be popped up on the screen. In order to achieve this purpose, the version, language settings, the unique identifier, the IP address of your computer and the hostname of VPN Server which is connected to will be sent to the SoftEther Update server. No personal information will be sent. Automatic Update Notification is enabled by default, however you can disable it on the configuration screen. The setting whether turned on or turned off will be saved individually corresponding to each destination VPN server, by VPN Server Manager.

2.8. Virtual NAT Function
A Virtual Hub on SoftEther VPN Server / Bridge has "Virtual NAT Function" . Virtual NAT Function can share a single IP address on the physical network by multiple private IP address of VPN Clients. There are two operation mode of Virtual NAT: User-mode and Kernel-mode. In the user-mode operation, Virtual NAT shares an IP address which is assigned on the host operating system. Unlike user-mode, the kernel-mode operation attempts to find DHCP servers on the physical network. If there are two or more physical networks, a DHCP server will be sought automatically for each segments serially. If a DHCP server found, and an IP address is acquired, the IP address will be used by the Virtual NAT. In this case, an IP entry as a DHCP client will be registered on the IP pool of the physical DHCP Server. The physical default gateway and the DNS server will be used by the Virtual NAT in order to communicate with hosts in Internet. In kernel-mode operation, a Virtual Hub has a virtual MAC address which is operating on the physical Ethernet segment. In order to check the connectivity to Internet, SoftEther VPN periodically sends DNS query packet to resolve the IP address of host "www.yahoo.com" or "www.baidu.com" , and attempts to connect to the TCP port 80 of such a resulted IP address for connectivity check.

2.9. Unattended Installation of Kernel-mode Components
When SoftEther VPN will detect a necessity to install the kernel-mode components on Windows, a confirmation message will be appeared by Windows system. In this occasion, SoftEther VPN software will switch to the Unattended Installation mode in order to respond "Yes" to Windows. This is a solution to prevent dead-locks when a remote-administration is performed from remote place.

2.10. Windows Firewall
SoftEther VPN software will register itself as a safe-program. Such an entry will be remain after the uninstallation. You can remove it manually from the Control Panel of Windows.


3. Internet Services
3.1. Internet Services which are provided by SoftEther Corporation
SoftEther Corporation provides Dynamic DNS, NAT Traversal and VPN Azure server services on the Internet. These services are free of charge. Customers can access to the services by using SoftEther VPN software, via Internet. These service will be planned to be available from Open-Source version of "SoftEther VPN" which will be released in the future.

3.2. Sent Information and Privacy Protection
SoftEther VPN software may send an IP address, hostname, the version of VPN software on the customer's computer to the cloud service operated by SoftEther Corporation, in order to use the above services. These sending of information are minimal necessary to use the services. No personal information will be sent. SoftEther Corporation records log files of the cloud service servers for 90 days at least with the received information. Such logs will be used for troubleshooting and other legitimate activities. SoftEther Corporation may provide logs to a public servant of Japanese government who are belonging to courts, police stations and the prosecutor's office, in order to comply such authorities' order. (Every Japanese public servants are liable by law to keep the information close.) Moreover, the IP addresses or other information will be processed statistically and provided to the public, not to expose the each concrete IP address, in order to release the release of research activities.

3.3. Communication Data via VPN Azure Service
Regardless of the above 3.2 rule, if the customer sends or receives VPN packets using VPN Azure Cloud Service, the actual payloads will stored and forwarded via the volatile memory of the servers for very short period. Such a behavior is naturally needed to provide the "VPN relay service" . No payloads will be recorded on "fixed" storages such as hard-drives. However, the "Wiretapping for Criminals Procedures Act" (The 137th legislation ruled on August 18, 1999 in Japan) requires telecommunication companies to allow the Japanese government authority to conduct a wire-tapping on the line. VPN Azure Servers which are physically placed on Japan are subjects of this law.

3.4. Comply to Japanese Telecommunication Laws
SoftEther Corporation complies with Japanese Telecommunication Laws as necessary to provide online services via Internet.

3.5. Free and Academic Experiment Services
SoftEther provides Dynamic DNS, NAT Traversal and VPN Azure as academic experiment services. Therefore, there services can be used for free of charge. These services are not parts of "SoftEther VPN Software Products" . These services are provided without any warranty. The services may be suspended or discontinued by technical or operational matters. In such occasions, users will not be able to use the services. A user have to understand such risks, and to acknowledge that such risks are borne by a user-self. SoftEther will never be liable to results or damages of use or unable-to-use of the service. Even if the user has already paid the license-fee of the commercial version of SoftEther VPN, such paid fees don't include any fees of these services. Therefore, if the online services will stop or be discontinued, no refunds or recoveries of damages will be provided by SoftEther Corporation.

3.6. DNS Proxy Cloud Servers
In some regions, when a user uses Internet, a DNS query sometimes broken or lost when it is passing through the ISP line. If SoftEther VPN Server, Client or Bridge detects a possibility that the accessing to the actual VPN server might be unstable, then DNS queries will be also transferred to the DNS proxy cloud servers which are operated by SoftEther Corporation. A DNS proxy cloud server will respond DNS queries with answering correct a IP address.


4. General Cautions
4.1. Needs an Approval from Network Administrator
SoftEther VPN has powerful functions which don't require special settings by network administrators. For example, you need not to ask the administrator to configure the existing firewall in order to "open" a TCP/UDP port. Such characteristic features are for the purpose to eliminate working times and costs of network administrators, and avoid misconfiguration-risks around the tasks to open specific exception ports on the firewall. However, any employees belong to the company have to obtain an approval from the network administrator before installs SoftEther VPN. If your network administrator neglects to provide such an approval, you can consider to take an approval from an upper authority. (For example, executive officer of the company.) If you use SoftEther VPN without any approvals from the authority of your company, you might have disadvantage. SoftEther Corporation will be never liable for results or damages of using SoftEther VPN.

4.2. Observe Laws of Your Country
If your country's law prohibits the use of encryption, you have to disable the encryption function of SoftEther VPN by yourself. Similarly, in some countries or regions, some functions of SoftEther VPN might be prohibited to use by laws. Other countries' laws are none of SoftEther Corporation's concern because SoftEther Corporation is an enterprise which is located and registered in Japan physically. For example, there might be a risk that a part of SoftEther VPN conflicts an existing patent which is valid only on the specific region. SoftEther Corporation has no interests in such specific region outside Japan's territory. Therefore, if you want to use SoftEther VPN in regions outside Japan, you have to be careful not to violate third-person's rights. You have to verify the legitimacy of the use of SoftEther VPN in the specific region before you actually use it in such region. By nature, there are almost 200 countries in the World, and each country's law is different each other. It is practically impossible to verify every countries' laws and regulations and make the software comply with all countries' laws in advance to release the software. Therefore SoftEther Corporation has verified the legitimacy of SoftEther VPN against the laws and regulations of only Japan. If a user uses SoftEther VPN in a specific country, and damaged by public servants of the government authority, SoftEther Corporation will never be liable to recover or compensate such damages or criminal responsibilities.


5. VPN Gate Academic Experiment Project
(This chapter applies only on SoftEther VPN software package which contains the extension plug-in for VPN Gate Academic Experiment Project.)
5.1. About VPN Gate Academic Experiment Project
VPN Gate Academic Experiment Project is an online service operated for just the academic research purpose at the graduate school of University of Tsukuba, Japan. The purpose of this research is to expend our knowledge about the "Global Distributed Public VPN Relay Server" (GDPVRS) technology. For details, please visit http://www.vpngate.net/.

5.2. About VPN Gate Service
SoftEther VPN Server and SoftEther VPN Client may contain "VPN Gate Service" program. However, VPN Gate Service is disabled by default.
VPN Gate Service should be activated and enabled by the voluntary intention of the owner of the computer which SoftEther VPN Server or SoftEther VPN Client is installed on. After you activate VPN Gate Service, the computer will be start to serve as a part of the Global Distributed Public VPN Relay Servers. The IP address, hostname and related information of the computer will be sent and registered to the directory server of VPN Gate Academic Experiment Project, and they will be published and disclosed to the public. This mechanism will allow any VPN Gate Client software's user to connect to the VPN Gate Service running on your computer. While the VPN session between a VPN Gate Client and your VPN Gate Service is established, the VPN Gate Client's user can send/receive any IP packets towards the Internet via the VPN Gate Service. The global IP address of the VPN Gate Service's hosing computer will be used as the source IP address of such communications which a VPN Gate Client initiates.
VPN Gate Service will send some information to the VPN Gate Academic Experiment Service Directory Server. The information includes the operator's information which described in section 5.5, logging settings, uptime, operating system version, type of protocol, port numbers, quality information, statistical information, VPN Gate clients' log history data (includes dates, IP addresses, version numbers and IDs) and the version of the software. These information will be exposed on the directory. VPN Gate Service also receives a key for encoding which is described on the chapter 5.9 from the directory server.

5.3. Details of VPN Gate Service's Behavior
If you enable VPN Gate Service manually, which is disabled by default, the "VPNGATE" Virtual Hub will be created on the SoftEther VPN Server. If you are using SoftEther VPN Client and attempt to active VPN Gate Service on it, an equivalent program to SoftEther VPN Server will be invoked on the same process of SoftEther VPN Client, and the "VPNGATE" Virtual Hub will be created. The "VPNGATE" Virtual Hub contains a user named "VPN" by default which permits anyone on the Internet to make a VPN connection to the Virtual Hub. Once a VPN Client connects to the "VPNGATE" Virtual Hub, any communication between the user and the Internet will pass through the Virtual Hub, and transmitted/received using the physical network interface on the computer which SoftEther VPN Server (or SoftEther VPN Client) is running on. This will cause the result that a destination host specified by the VPN Client will identify that the source of the communication has initiated from the VPN Gate Service's hosting computer's IP address. However, for safety, any packets which destinations are within 192.168.0.0/255.255.0.0, 172.16.0.0/255.240.0.0 or 10.0.0.0/255.0.0.0 will be blocked by the "VPNGATE" Virtual Hub in order to protect your local network. Therefore, if you run VPN Gate Service on your corporate network or private network, it is safe because anonymous VPN Client users will not be permitted to access such private networks. VPN Gate Service also serves as relay for accessing to the VPN Gate Directory Server.
In order to make VPN Gate Service familiar with firewalls and NATs, it opens an UDP port by using the NAT Traversal function which is described on the section 1.2. It also opens and listens on some TCP ports, and some TCP and UDP ports will be specified as the target port of Universal Plug and Play (UPnP) Port Transfer entries which are requested to your local routers. UPnP request packets will be sent periodically. Some routers keep such an opened TCP/UDP port permanently on the device. If you wish to close them, do it manually.
VPN Gate Service also provides the mirror-site function for www.vpngate.net. This is a mechanism that a copy of the latest contents from www.vpngate.net will be hosted by the mirror-site tiny HTTP server which is running on the VPN Gate Service program. It will register itself on the mirror-sites list in www.vpngate.net. However, it never relays any other communications which are not towards www.vpngate.net.

5.4. Communication between Internet via VPN Gate Service
VPN Gate Service provides a routing between users and the Internet, by using the Virtual NAT Function which is described on the section 2.8. VPN Gate Service sends polling Ping packets to the server which is located on University of Tsukuba, and the Google Public DNS Server which is identified as 8.8.8.8, in order to check the latest quality of your Internet line. VPN Gate Service also sends and receives a lot of random packets to/from the Speed Test Server on University of Tsukuba. These quality data will be reported to VPN Gate Directory Server, automatically and periodically. The result will be saved and disclosed to the public. These periodical polling communication are adjusted not to occupy the Internet line, however in some circumstances they might occupy the line.

5.5. Operator's Information of VPN Gate Service
If you activate VPN Gate Service on your computer, the computer will be a part of the Global Distributed Public VPN Relay Servers. Therefore, the Operator's administrative information of your VPN Gate Service should be reported and registered on the VPN Gate Service Directory. Operator's information contains the name of the operator and the abuse-reporting contact e-mail address. These information can be inputted on the screen if the VPN Gate configuration. Inputted information will be transmitted to the VPN Gate Directory Server, stored and disclosed to the public. So you have to be careful to input information. By the way, until you specify something as the operator's information, the computer's hostname will be used automatically as the field of the name of the operator, by appending the "'s owner" string after the hostname.

5.6. Observe Laws to Operate VPN Gate Service
In some countries or regions, a user who is planning to activate and operate VPN Gate Service, he are mandated to obtain a license or register a service from/to the government. If your region has such a regulation, you must fulfill mandated process before activating VPN Gate Service in advance. Neither the developers nor operators of the VPN Gate Academic Experiment Project will be liable for legal/criminal responsibilities or damages which are occurred from failure to comply your local laws.

5.7. Protect Privacy of Communication
Most of countries have a law which requires communication service's operators, including VPN Gate Service operators, to protect the privacy of communication of third-persons. When you operate VPN Gate Service, you must always protect user's privacy.

5.8. Packet Logs
The packet logging function is implemented on VPN Gate Service. It records essential headers of major TCP/IP packets which are transmitted via the Virtual Hub. This function will be helpful to investigate the "original IP address" of the initiator of communication who was a connected user of your VPN Gate Service, by checking the packet logs and the connection logs. The packet logs are recorded only for such legitimate investigates purpose. Do not peek nor leak packet logs except the rightful purpose. Such act will be violate the section 5.7.

5.9. Packet Logs Automatic Archiving and Encoding Function
The VPN Gate Academic Experiment Service is operated and running under the Japanese constitution and laws. The Japanese constitution laws demand strictly protection over the privacy of communication. Because this service is under Japanese rules, the program of VPN Gate Service implements this "Automatic Log File Encoding" protection mechanism, and enabled by default.
The VPN Gate Service is currently configured to encode packet log files which has passed two or more weeks automatically, by default. In order to protect privacy of communication, if a packet log file is once encoded, even the administrator of the local computer cannot censor the packet log file. This mechanism protects privacy of end-users of VPN Gate Service.
You can change the VPN Gate Service setting to disable this automatic encoding function. Then packet log files will never be encoded even after two weeks passed. In such a configuration, all packet logs will remain as plain-text on the disk. Therefore you have to take care not to violate user's privacy.
If you are liable to decode an encoded packet log files (for example: a VPN Gate Service's user illegally abused your VPN Gate Service and you have to decode the packet logs in order to comply the laws), contact the administrator of the VPN Gate Academic Experiment Service at Graduate School of University of Tsukuba, Japan. You can find the contact address at http://www.vpngate.net/. The administrator of VPN Gate Service will respond to decode the packet logs if there is an appropriate and legal request from court or other judicial authorities, according to laws.

5.10. Caution if You Operate VPN Gate Service in the Japan's Territories
When a user operates VPN Gate Service in the Japan's territories, such an act may be regulated under the Japanese Telecommunication Laws if the operation is a subject to the law. However, in such a circumstance, according to the "Japanese Telecommunication Business Compete Manual [supplemental version]" , non- profitable operations of communications are not identified as a "telecommunication business" . So usual operators of VPN Gate Service are not subjects to "telecommunication business operators" , and not be mandated to register to the government. Even so, legalities to protect the privacy of communication still imposed. As a conclusion, if you operate VPN Gate Service in the Japan's Territories, you must not leak the secrets of communications which are transmitted via your operating VPN Gate Service.

5.11. VPN Gate Client
If SoftEther VPN Client contains the VPN Gate Client plug-in, you can use it to obtain the list of current operating VPN Gate Service servers in the Internet, and make a VPN connection to a specific server on the list.
VPN Gate Client always keeps the latest list of the VPN Gate Services periodically. Be careful if you are using a pay-per-use Internet line.
When you start the VPN Gate Client software, the screen which asks you activate or not VPN Gate Service will be appeared. For details of VPN Gate Service, read the above sections.

5.12. Caution before Joining or Exploiting VPN Gate Academic Experiment Project
The VPN Gate Academic Experiment Service is operated as a research project at the graduate school on University of Tsukuba, Japan. The service is governed under the Japanese laws. Other countries' laws are none of our concerns nor responsibilities.
By nature, there are almost 200 countries in the World, with different laws. It is impossible to verify every countries' laws and regulations and make the software comply with all countries' laws in advance to release the software. If a user uses VPN Gate service in a specific country, and damaged by public servants of the authority, the developer of either the service or software will never be liable to recover or compensate such damages or criminal responsibilities.
By using this software and service, the user must observe all concerned laws and rules with user's own responsibility. The user will be completely liable to any damages and responsibilities which are results of using this software and service, regardless of either inside or outside of Japan's territory.
If you don't agree nor understand the above warnings, do not use any of VPN Gate Academic Experiment Service functions.
VPN Gate is a research project for just academic purpose only. VPN Gate was developed as a plug-in for SoftEther VPN and UT-VPN. However, all parts of VPN Gate were developed on this research project at University of Tsukuba. Any parts of VPN Gate are not developed by SoftEther Corporation. The VPN Gate Research Project is not a subject to be led, operated, promoted nor guaranteed by SoftEther Corporation.

5.13. The P2P Relay Function in the VPN Gate Client to strengthen the capability of circumvention of censorship firewalls
VPN Gate Clients, which are published since January 2015, include the P2P Relay Function. The P2P Relay Function is implemented in order to strengthen the capability of circumvention of censorship firewalls. If the P2P Relay Function in your VPN Gate Client is enabled, then the P2P Relay Function will accept the incoming VPN connections from the VPN Gate users, which are located on mainly same regions around you, and will provide the relay function to the external remote VPN Gate Servers, which are hosted by third parties in the free Internet environment. This P2P Relay Function never provides the shared NAT functions nor replaces the outgoing IP address of the VPN Gate users to your IP addresses because this P2P Relay Function only provides the "reflection service" (hair-pin relaying), relaying from incoming VPN Gate users to an external VPN Gate Server. In this situation, VPN tunnels via your P2P Relay Function will be finally terminated on the external VPN Gate Server, not your VPN Gate Client. However, the VPN Gate Server as the final destination will record your IP address as the source IP address of VPN tunnels which will be initiated by your P2P Relay Function. Additionally, user packets which are transmitted via your P2P Relay Function will be recorded on your computer as packet logs as described on the section 5.8. After you installed the VPN Gate Client, and if the P2P Relay Function will be enabled automatically, then all matters on the 5.2, 5.3, 5.4, 5.5, 5.6, 5.7, 5.8, 5.9, 5.10, 5.11 and 5.12 sections will be applied to you and your computer, as same to the situation when you enabled the VPN Gate Service (the VPN Gate Server function). If your P2P Function is enabled, then your computer's IP address and the default operator's name which is described on the section 5.5 will be listed on the VPN Gate Server List which is provided by the VPN Gate Project. You can change these strings by editing the "vpn_gate_relay.config" file manually. Note that you need to stop the VPN Client service before editing it. The VPN Gate Client will automatically enable the P2P Relay Function on your computer if the VPN Gate Client detects that your computer might be located in regions where there are existing censorship firewalls. If you want to disable the P2P Relay Function, you must set the "DisableRelayServer" flag to "true" on the "vpn_client.config" file which is the configuration file of the VPN Client. Note that you need to stop the VPN Client service before editing it. The VPN Gate Client does not recognize the particular regulation of your country or your region. The VPN Gate Client activates the P2P Relay Function even if your country or your region has the law to restrict running P2P relay functions. Therefore, in such a case, you must disable the P2P Relay Function on the VPN Gate Client manually by setting the "DisableRelayServer" flag if you reside in such a restricted area, in your own responsibility.


---

关于 SoftEther VPN 的重要声明

嵌入在本软件的 VPN 通信功能比以往任何时候都要强大。这个强大的 VPN 能力将为您带来巨大的好处。然而，如果你滥用此软件， IT 可能会损害你自己。为了避免这样的风险，本文档为愿意使用本软件的客户公布了重要提示。下面的说明是非常重要的。仔细阅读并理解它。


1. VPN 通信协议
1.1. SoftEther VPN 协议
SoftEther VPN 可以进行 VPN 通信。不同于传统的 VPN 协议， SoftEther VPN 有一个全新设计的 "SoftEther VPN 协议 (SE-VPN 协议)" 的实现。SE-VPN 协议将任何以太网数据包封装进 HTTPS (HTTP over SSL) 连接。因此 SE-VPN 协议可以越过防火墙通信，即使防火墙被网络管理员配置阻止传统的 VPN 数据包。SE-VPN 协议的设计和实施以符合 TLS 1.0 (RFC 5246) 和 HTTPS (RFC 2818)。然面，有时对 RFC 有不同的行为。如果你是一个网络管理员，要在防火墙上阻止 SE-VPN 协议，你可以在防火墙上采取 "白名单" 策略，来过滤任何在边界上的 TCP 或 UDP 数据包，除了明确允许到特定网站和服务器的数据包。

1.2. NAT 穿透功能
一般来说，如果你使用传统的 VPN 系统，你必须要求网络管理员把 NAT 或防火墙设置为 "打开" 或 "中继" 特定的 TCP 或 UDP 端口。然而，也有需要以某种方式消除网络管理员的这种工作成本。为了满足这种需求， SoftEther VPN 有一个新实施的 "NAT 穿越" 功能。NAT 穿越默认情况下是启用的。一个在 NAT 或防火墙后面、在电脑上运行的 SoftEther VPN 服务器可以接受来自互联网的 VPN 连接，在防火墙或 NAT 上没有任何特殊的配置。如果你想禁用 NAT 穿越功能，修改 SoftEther VPN 服务器上的配置文件 "DisableNatTraversal" 为 "true" 。为了在客户端禁用它，在目标主机添加 "/ tcp" 后缀。

1.3. 动态 DNS 功能
传统的 VPN 系统在 VPN 服务器上需要一个静态全球 IP 地址。鉴于全球 IP 地址的短缺， SoftEther 公司在 SoftEther VPN 服务器上实施了 "动态 DNS 功能" 。动态 DNS 是默认启用的。动态 DNS 功能通知计算机的当前全球 IP 地址到由 SoftEther 公司操作的动态 DNS 服务器。一个全球唯一主机名 (FQDN) ，如 "abc.softether.net" ( "ABC" 随每个用户唯一而不同) 将在 VPN 服务器上被指定。如果你告诉一个 VPN 用户这个唯一的主机名，用户可以在 VPN 客户端上将其指定为目标 VPN 服务器的主机名，将能连接到 VPN 服务器。事先无需知道 IP 地址。如果 VPN 服务器的 IP 地址变化了，相关动态 DNS 服务的主机名注册的 IP 地址会自动改变。通过这种机制，不再需要每月向 ISP 缴费的全球静态 IP 地址。您可以使用带动态 IP 地址的、消费者级、廉价的互联网连接，来操作一个企业级的 VPN 系统。如果你想禁用动态 DNS ，把 SoftEther VPN 服务器配置文件中的 "DDnsClient" 指令的 "Disabled" 项目指定为 "true" 。* 中华人民共和国的居民请注意:如果你的 VPN 服务器运行在中华人民共和国， DNS 后缀将被替换为 "sedns.cn" 域名。 "sedns.cn" 域名服务由 "北京大游索易科技有限公司" 拥有和运营的，它是一个中国本地的企业。

1.4. VPN over ICMP / VPN over DNS 功能
如果你想在 SoftEther VPN 客户端 / 网桥和 SoftEther VPN 服务器之间建立一个 VPN 连接，但如果 TCP 和 UDP 数据包被防火墙禁止通过，那么你可以把有效载荷封装进 "ICMP" (被称为 Ping) 或 "DNS" 数据包。通过使用 ICMP 或 DNS ，即使防火墙或路由器阻止每个 TCP 或 UDP 连接，此功能可以实现 VPN 连接。VPN over ICMP/ VPN over DNS 功能尽可能的设计符合标准 ICMP 和 DNS 规范，但有时也不完全符合他们的行为。因此，一些劣质路由器可能会导致内存溢出或当有很多 ICMP 或 DNS 数据包通过时产生麻烦，这种路由器有时死机或重新启动。它可能会影响在同一网络上的其他用户。为了避免这样的风险，在 VPN 客户端指定的目标主机名上附加后缀 "/tcp" ，禁用 VPN over ICMP / DNS 功能。

1.5. VPN Azure 云服务
如果您的 SoftEther VPN 服务器放置在 NAT 或防火墙后面，由于某种原因，你不能使用 NAT 穿透功能、动态 DNS 功能或 VPN over ICMP/DNS 功能，您可以使用 VPN Azure Clouse 服务。 SoftEther 公司在互联网上运行 VPN Azure 云。VPN 服务器连接到 VPN Azure 云，主机名 "abc.vpnazure.net" ( "abc" 是一个唯一的主机名) 通过 VPN Azure 云可以被指定连接到 VPN 服务器。实际上，这样的一个主机名指向一个由 SoftEther 公司所操作的云服务器的全球 IP 地址。如果一个 VPN 客户端连接到一个 VPN Azure 主机，那么 VPN Azure 主机转播在 VPN 客户端和 VPN 服务器之间的所有流量。VPN Azure 在默认情况下是禁用的。您可以通过使用 VPN 服务器配置工具很容易地激活它。

1.6. UDP 加速
SoftEther VPN 具有 UDP 加速功能。如果一个 VPN 是由两个站点组成检测到 UDP 通道已建立， UDP 将自动使用。通过此功能， UDP 的吞吐量增加了。如果直接的 UDP 通道已被建立，直接的 UDP 数据包将被使用。但是，如果有一些障碍，如防火墙或 NAT ， "UDP 冲孔" 技术将被使用。 "UDP 冲孔" 使用 SoftEther 公司在互联网上操作的云服务器。UDP 加速通过在 VPN 客户端一侧进行设置在任何时候可以被禁用。


2. VPN 软件
The notes in this section are not specific to SoftEther VPN or VPN Gate, but apply to general system software. SoftEther VPN Client, SoftEther VPN Server, SoftEther VPN Bridge, and VPN Gate Relay Service will be installed on your computer as system services. System services always run in the background. System services usually do not appear on the computer display. Then your computer system is booted, system services automatically start in the background even before you or other users log in. To check whether SoftEther-related system service is running, check the process list or the background service list of your OS (called as "Services" in Windows, or "Daemons" in UNIX.) You can activate, deactivate, start, or stop system services using the functions of the OS anytime. SoftEther-related GUI tools for managing system services communicate with these system services. After you terminate these management GUI tools, SoftEther-related system services will continue to run in the background. System services consume CPU time, computer power, memory and disk space. Because system services consume power, your electricity charges and amount of thermal of your computer increase as result. In addition, there is a possibility that the mechanical parts of the life of your computer is reduced.

2.1. SoftEther VPN 客户端
如果您在 Windows 上使用 SoftEther VPN 客户端，虚拟网络适配器设备驱动程序将安装在 Windows 上。虚拟网络适配器作为一个内核模式驱动程序实施在 Windows 上。驱动程序是数字签名的，由 VeriSign ， Inc 所签发的证书，还由 Symantec Corporation (赛门铁克公司) 签署。问你要确保安装驱动程序的一条消息可能会弹出在屏幕上。如果可能的话， SoftEther VPN 客户端可能会响应消息。SoftEther VPN 客户端还优化了在 Windows 上 MMCSS (多媒体类计划程序服务) 的配置。您以后可以撤消 MMCSS 的优化。

2.2. SoftEther VPN 服务器 / 网桥
如果您使用 SoftEther VPN 服务器 / 网桥在 Windows 上的 "本地网桥" 功能，你必须在电脑上安装低级别的以太网数据包处理驱动程序。驱动程序是数字签名的，由 VeriSign ， Inc 所签发的证书，还由 Symantec Corporation (赛门铁克公司) 签署。SoftEther VPN 服务器 / 网桥在物理网络适配器本地网桥功能中可以禁用 TCP / IP 卸载特性。在 Windows Vista /2008 或更高版本， VPN 服务器可以注入一个符合 Windows 过滤平台 (WPF) 规范的数据包过滤驱动程序至内核以提供 IPsec 功能。数据包过滤驱动程序将被加载仅当启用 IPsec 功能时。一旦您启用 SoftEther VPN 服务器的 IPsec 功能， Windows 内置的 IPsec 功能将被禁用。在您禁用了 SoftEther VPN 服务器的 IPsec 功能之后，那么 Windows 内置的 IPsec 功能将复苏。为了提供本地桥功能， SoftEther VPN 服务器 / 网桥在操作系统上禁用 TCP / IP 卸载功能。

2.3. 用户模式安装
您可以在 Windows 以 "用户模式" 安装 SoftEther VPN 服务器和 SoftEther VPN 网桥。换句话说，即使你没有 Windows 系统管理员的权限，你可以作为一个普通用户安装 SoftEther VPN。用户模式安装将禁用一些功能，但其他大部分功能都能正常工作。因此，例如，雇员可以在办公室网络中的计算机上安装 SoftEther VPN 服务器端，他将能够从他家连接到服务器。为了由用户自己实现这样的系统，在技术观点上无须系统管理员权限。然而，违反公司规定未经授权在计算机上安装软件可能会被视为不受欢迎的行为。如果你是一名雇员属于该公司，该公司的政策禁止安装软件或未经允许进行互联网通信，你必须事先从网络管理员或您公司的总裁获得许可，再安装 SoftEther VPN。如果您以用户模式安装 VPN 服务器 / 网桥，图标将出现在 Windows 任务托盘。如果您觉得该图标妨碍你了，你可以操作将其隐藏。然而，你不能利用此隐藏功能在其他人的电脑上安装 VPN 服务器作为间谍软件。这种行为可能是违反刑法的犯罪。

2.4. 保持活跃功能
默认情况下， SoftEther VPN 服务器和 SoftEther VPN 网桥有保持活跃的功能。此功能的目的是为了维持互连网线路的活跃。该功能定期发送带有随机 - 字节 - 数组 - 有效载荷的 UDP 数据包。此功能为避免移动或拨号连接的自动断开是非常有用的。您可以随时禁用保持活跃功能。

2.5. 卸载
SoftEther VPN 软件的卸载过程将删除所有程序文件。然而，非程序文件 (如程序运行所产生的文件和数据) 将不会被删除。由于技术原因，卸载程序的 exe 和资源文件可能仍然存在。这些剩余的文件决不会影响使用计算机，但是你可以手动删除它。内核模式驱动程序可能不会被删除，但是这样的驱动程序在 Windows 下次启动时不会被加载。您可以使用 Windows 的 "sc" 命令手动删除内核模式驱动程序。

2.6. 安全
你应该在安装后在 SoftEther VPN 服务器 / 网桥设置管理员的密码。如果你没有做到这一点，其他人未经您许可可以访问 SoftEther VPN 服务器 / 网桥，并可以设置密码。这个警告可能也适用于 Linux 版本的 SoftEther VPN 客户端。

2.7. 自动更新通知
Windows 版的 SoftEther VPN 软件有自动更新通知功能。它定期访问 SoftEther 更新服务器检查是否发布了最新版本的软件。如果最新版已发布，通知消息将在屏幕上弹出。为了达到这个目的，版本、语言设置、您的计算机的 IP 地址、唯一标识符、连接到 VPN 服务器的主机名将被发送到 SoftEther 的更新服务器。任何个人信息将不被发送。默认情况下自动更新通知是启用的，然而你可以在配置屏幕上禁用它。通过 VPN 服务器管理器，设置是否打开或关闭将被单独保存对应每个目标 VPN 服务器。

2.8. 虚拟 NAT 功能
虚拟 HUB 在 SoftEther VPN 服务器 / 网桥上有 "虚拟 NAT 功能" 。虚拟 NAT 功能可以通过 VPN 客户端的多个私有 IP 地址共享同一个物理网络上的单一 IP 地址。有两种虚拟 NAT 的操作模式:用户模式和内核模式。在用户模式下运行，虚拟 NAT 共享主操作系统上分配的一个 IP 地址。不同于用户模式，内核模式的操作试图找到物理网络上的 DHCP 服务器。如果有两个或以上的物理网络，每个网段上的 DHCP 服务器会被自动连续寻找。如果发现 DHCP 服务器，并获取一个 IP 地址， IP 地址将被虚拟 NAT 使用。在这种情况下，作为 DHCP 客户端的 IP 条目将被登记在物理 DHCP 服务器的 IP 池。为了在互连网中和主机进行通信，物理默认网关和 DNS 服务器将被虚拟 NAT 使用。在内核模式的操作中，虚拟 HUB 上有一个运行在物理以太网段上的虚拟 MAC 地址。
为了检查到互联网的连通性， SoftEther VPN 定期发送 DNS 查询数据包，以解析 "www.yahoo.com" 或 "www.baidu.com" 主机的 IP 地址，并尝试连接到这样结果 IP 地址的 TCP 80 端口，进行连通性检查。

2.9. 内核模式组件的无人值守安装
当 SoftEther VPN 检测到需要在 Windows 安装内核模式组件， Windows 系统将出现一条确认消息。在此之际， SoftEther VPN 软件将切换到无人值守的安装模式，以回应 "是" 到 Windows。当从遥远地点进行远程管理时，这个解决方案可以防止锁死。

2.10. Windows 防火墙
SoftEther VPN 软件将其自身注册为一个安全程序。这样的条目在卸载后仍被保留。您可以从 Windows 的控制面板中手动删除它。


3. 互连网服务
3.1. SoftEther 公司提供的互连网服务
SoftEther 公司在互联网上提供了动态 DNS、NAT 穿透、和 VPN Azure 服务器服务。这些服务都是免费的。客户通过使用 SoftEther VPN 软件，经由互联网访问这些服务。这些服务计划将在以后发布的 "SoftEther VPN" 的开源版本中也提供。

3.2. 发送的信息和隐私保护
为了使用上述服务， SoftEther VPN 软件可以从客户的计算机到由 SoftEther 公司操作的云服务发送 IP 地址、主机名、VPN 软件的版本。这些信息的发送是要使用这些服务的最少必须内容。无任何个人信息将被发送。 SoftEther 公司记录接收到的最少信息在云服务服务器的日志文件为 90 天。这些日志将被用于故障排除和其他合法活动。SoftEther 公司可以提供日志给属于法院、警察局和检察院的日本政府的公务人员，以遵守当局的命令。(每一个日本公务人员有责任根据法律密切保存这些信息。) 此外， IP 地址或其他信息将进行统计处理，并提供给公众，而不是暴露每一个具体的 IP 地址，以进行研究活动的发布。

3.3. 通过 VPN Azure 服务的通信数据
不管以上 3.2 的规则，如果客户使用 VPN Azure 云服务的发送或接收 VPN 数据包，实际的有效载荷将在很短的时间通过服务器的易失性存储器存储和转发。这样的行为自然需要提供 "VPN 中继服务" 。无有效载荷将被记录在 "固定的" 储存设备，如硬盘驱动器。然而， "窃听罪犯程序法" (日本在 1999 年 8 月 18 日裁决的第 137 个立法) 要求电信公司允许日本政府当局进行在线窃听。物理放置在日本的 VPN Azure 服务器也是服从于这个法律。

3.4. 符合日本电信法
SoftEther 公司符合日本电信法必要时通过互联网提供在线服务。

3.5. 免费和学术实验服务
SoftEther 作为学术实验服务提供动态 DNS、NAT 穿透和 VPN Azure。因此，服务可以被用于免费。这些服务不是 "SoftEther VPN 软件产品" 的一部分。这些服务不提供任何保证。这些服务由于技术或操作问题可能会被暂停或终止。在这种情况下，用户将无法使用这些服务。用户必须了解这些风险，并承认由用户自行承担这样的风险。SoftEther 永远不会对结果、或使用的损害、或服务无法使用承担任何责任。即使用户已经支付 SoftEther VPN 商业版的许可费用，因为支付的费用不包含这些服务的任何费用。因此，如果在线服务将停止或终止， SoftEther 公司将不提供任何退款或损害的补偿。

3.6. DNS 代理云服务器
在某些地区，当用户使用互连网，通过 ISP 线路时，一个 DNS 查询有时损坏或丢失。如果 SoftEther VPN 的服务器、客户端或网桥检测到访问实际的 VPN 服务器可能不稳定的可能性，那么 DNS 查询将被转移到由 SoftEther 公司运行的 DNS 代理云服务器。DNS 代理云服务器将回答纠正一个 IP 地址响应 DNS 查询。


4. 一般注意事项
4.1. 需要网络管理员的批准
SoftEther VPN 具有强大的功能，不需要网络管理员的特殊设置。例如，您不必要求管理员配置现有的防火墙以 "打开" TCP / UDP 端口。这些性能特点是为了以下目的:消除网络管理员的工作时间和成本，并避免误配置风险，如在防火墙上打开特定的异常端口的任务。然而，在安装 SoftEther VPN 前，属于公司的任何员工必须获得网络管理员的批准。如果您的网络管理员忽略提供这样的批准，你可以考虑获得上级领导的批准。(例如，该公司总裁。) 如果您没有获得公司领导的批准使用 SoftEther VPN ，你可能有不利的条件。SoftEther 公司将不会对使用 SoftEther VPN 的结果或损害承担责任。

4.2. 遵守贵国的法律
如果您所在国家的法律禁止加密的使用，你自己必须禁用 SoftEther VPN 的加密功能。同样，在一些国家或地区， SoftEther VPN 的某些功能可能会被法律禁止使用。其他国家的法律与 SoftEther 公司无关，因为 SoftEther 公司是一个在物理上位于并注册于日本的企业。例如，可能存在一种风险，即 SoftEther VPN 的一部分与只在某些特定区域有效的现有专利冲突。SoftEther 公司没有在日本固有领土之外这些特定区域的利益。因此，如果你想在日本以外的地区使用 SoftEther VPN ，你必须要小心不要侵犯第三人的权利。在您在这样的地区实际使用之前，您必须验证在这些特定区域使用 SoftEther VPN 的合法性。本来，在世界上有近 200 个国家，每个国家的法律都是不同的。这几乎是不可能的事先验证每一个国家的法律和法规，使软件符合所有国家的法律，再发布软件。因此 SoftEther 公司已核实 SoftEther VPN 仅对日本法律和法规的合法性。如果用户在一个特定的国家使用 SoftEther VPN ， SoftEther 公司将不会赔偿政府当局的损害，也不会承担恢复或赔偿此类损害或刑事法律责任。


5. VPN Gate 学术实验项目
(本章仅适用于 SoftEther VPN 软件包，其中包含 VPN Gate 学术实验项目的扩展插件。)
5.1. 关于 VPN Gate 学术实验项目
VPN Gate 学术实验项目是一个在线服务，由日本筑波大学研究生院为学术研究目的运营。本研究的目的是要扩大我们对 "全球分布式公共 VPN 中继服务器" 技术 (Global Distributed Public VPN Relay Server, GDPVRS) 的认识。有关详细信息，请访问 http://www.vpngate.net/。

5.2. 关于 VPN Gate 服务
SoftEther VPN 服务器和 SoftEther VPN 客户端可能含有 "VPN Gate 服务" 程序。然而， VPN Gate 服务在默认情况下是禁用的。
VPN Gate 服务通过安装了 SoftEther VPN 服务器或 SoftEther VPN 客户端的计算机所有者的志愿目的被激活并启用。在您激活 VPN Gate 服务以后，计算机将作为全球分布式公共 VPN 中继服务器的一部分开始服务。计算机的 IP 地址、主机名和相关信息将被发送并在 VPN Gate 学术实验项目的服务器目录注册，这些信息将被公布，并向公众披露。这一机制将允许任何 VPN Gate 客户端软件的用户连接到您计算机上运行的 VPN Gate 服务。当在 VPN Gate 客户端和你的 VPN Gate 服务之间建立一个 VPN 会话， VPN Gate 客户端的用户可以发送 / 接收向互联网经由 VPN Gate 服务的任何 IP 数据包。VPN Gate 服务的主机的全球 IP 地址将作为 VPN Gate 客户端启动的这种通信的源 IP 地址被使用。
VPN Gate 服务将发送一些信息至 VPN Gate 学术实验服务目录服务器。这些信息包括第 5.5 节中描述的运营商的信息、日志设置、正常运行时间、操作系统版本、协议类型、端口号、质量信息、统计信息、VPN Gate 客户端的日志历史数据 (包括日期，IP 地址，版本号和 ID) 和软件的版本。这些信息将被批露在目录上。VPN Gate 服务从目录服务器接收到一个密钥以进行在 5.9 章中描述的编码。

5.3. VPN Gate 服务行为的详细信息
如果您手动启用 VPN Gate 服务，在默认情况下是禁用的， "VPNGATE" 虚拟 Hub 将在 SoftEther VPN 服务器上被创建。如果您使用的是 SoftEther VPN 客户端，并尝试激活 VPN Gate 服务，相当于 SoftEther VPN 服务器的程序在 SoftEther VPN 客户端的同一进程将被调用，虚拟 HUB "VPNGATE" 将被创建。虚拟 HUB "VPNGATE" 包含一个默认情况下名为 "VPN" 的用户，此用户允许在互联网上的任何人建立 VPN 连接到虚拟 HUB。一旦 VPN 客户端连接到虚拟 HUB "VPNGATE" ，用户与互联网之间的任何通信将穿过虚拟 Hub ，使用运行有 SoftEther VPN 服务器 (或 SoftEther VPN 客户端) 的计算机上的物理网络接口发送 / 接收。这将导致以下结果，目标主机通过 VPN 客户端确定通信的源发起是从 VPN Gate 服务的主机的 IP 地址指定的。不过，为了安全，目的地是在 192.168.0.0/255.255.0.0 ， 172.16.0.0/255.240.0.0 或 10.0.0.0/255.0.0.0 以内的任何数据包将被虚拟 HUB "VPNGATE" 拦截，以保护您的本地网络。因此，如果在您的企业网络或私人网络运行 VPN Gate 服务，这是安全的，因为匿名 VPN 客户端用户将不被允许访问这些私人网络。VPN Gate 服务也可作为中继访问 VPN Gate 目录服务器。
为了使 VPN Gate 服务熟悉防火墙和 NAT ，通过使用 1.2 章描述的 NAT 穿透功能打开一个 UDP 端口。还打开了一些 TCP 端口并监听，一些 TCP 和 UDP 端口将被指定为本地路由器要求的通用即插即用 (UPnP) 传输条目的目标端口。UPnP 请求数据包将被定期发送。有些路由器在设备上永久保持一个开放的 TCP/UDP 端口。如果你想关闭他们，可以手动关闭。
VPN Gate 服务还提供了镜像网站功能 www.vpngate.net。这是一种机制，将的最新内容 www.vpngate.net 的副本被托管的镜像站点微小的 HTTP 服务器上运行的 VPN Gate 服务程序。它都将自己注册上镜的站点列表中 www.vpngate.net。然而，它从来不向 www.vpngate.net 任何其他通讯中继。

5.4. 互联网之间经由 VPN Gate 服务的通信
VPN Gate 服务提供了一个用户与互联网之间的路由，通过使用 2.8 章虚拟 NAT 功能。VPN Gate 服务发送 Ping 查询数据包到位于筑波大学的服务器，和被确定为 8.8.8.8 的谷歌公共 DNS 服务器，以检查您的互联网线路的最新质量。VPN Gate 服务还发送和接收大量的随机数据包到 / 从筑波大学的速度测试服务器上。这些高质量的数据将自动地、定期地被报告给 VPN Gate 目录服务器。结果将被保存并向公众披露。这些定期的查询通信被调整，尽量不占用互联网线路，但在某些情况下可能会占用线路。

5.5. VPN Gate 服务的运营商信息
如果您激活您计算机上的 VPN Gate 服务，此计算机将成为全球分布式公共 VPN 中继服务器的一部分。因此，您的 VPN Gate 服务的运营商管理信息应被报告和注册到 VPN Gate 服务目录里。运营商的信息包含了运营商的名称、滥用报告、联系的 e-mail 地址。这些信息可以被输入到屏幕上的 VPN Gate 配置里。输入的信息将被发送到 VPN Gate 目录服务器，保存并向公众披露。所以，你必须要小心地输入信息。顺便说一下，直到你指定某名称作为运营商的信息，计算机的主机名会被自动使用作为运营商名称的字段，通过在主机名后附加 "'s owner" 字符串。

5.6. 遵守法律运营 VPN Gate 服务
在某些国家或地区，正打算激活和运行 VPN Gate 服务的用户，他被强制要求从 / 到政府获得许可或注册服务。如果您所在的地区有这样的规定，你必须在激活 VPN Gate 服务之前，提前完成强制流程。无论是 VPN Gate 学术实验项目的开发者和运营商对于发生的未能遵守当地法律的法律 / 刑事责任或损害都不承担任何责任。

5.7. 保护通信的隐私
大多数国家有一个法律要求通信服务的运营商，包括 VPN Gate 服务运营商，以保障第三方的通信隐私。当您运营 VPN Gate 服务时，你必须始终保护用户的隐私。

5.8. 数据包日志
数据包日志功能在 VPN Gate 服务上实施。它记录通过虚拟 HUB 传输的主要 TCP/IP 数据包的基本包头。此功能将有助于了解连接您的 VPN Gate 服务用户的通信发起者的 "原始 IP 地址" ，通过检查数据包日志和连接日志。数据包日志记录的仅为合法调查的目的。不会偷看，也不会泄漏数据包日志，除非正当的目的。这种行为将违反 5.7 章。

5.9. 数据包日志的自动存档和编码功能
VPN Gate 学术实验服务是根据日本宪法和法律运营和运行的。日本宪法法律要求严格保护通信的隐私权。由于这项服务是根据日本的规则， VPN Gate 服务的程序实现了此 "自动日志文件编码" 的保护机制，并默认启用。
默认情况下， VPN Gate 服务当前自动配置编码已经过去了两周或以上的数据包日志文件。为了保护通信隐私，如果一个数据包日志文件一旦被编码，即使是本地计算机管理员也无法检查数据包日志文件。这种机制保护 VPN Gate 服务最终用户的隐私。
您可以更改 VPN Gate 服务的设置，禁用此项自动编码功能。然后数据包日志文件将永远不会被编码，即使两个星期已过去。在这样的配置中，所有数据包日志将以纯文本形式保留在磁盘上。因此，你必须要注意不要侵犯用户的隐私。
如果你负责解码已编码的数据包日志文件 (例如:一个 VPN Gate 服务的用户非法滥用你的 VPN Gate 服务，你必须解码数据包日志以符合法律) ，请联系日本筑波大学研究生院 VPN Gate 学术实验服务的管理员。你可以从 http://www.vpngate.net/ 找到联系地址。根据法律如果有从法院或其他司法当局适当的和法律的要求， VPN Gate 服务的管理员将响应解码数据包日志。

5.10. 在日本领土操作 VPN Gate 服务的注意事项
当一个用户在日本领土操作 VPN Gate 服务时，这种行为会根据日本电信法加以规范，操作受法律管辖。然而，在这样的情况下，根据 "日本电信业务竞争手册 [补充版本]" ，非营利性的通信业务不被认为是 "电信业务" 。因此，通常 VPN Gate 服务的运营商不受制于 "电信业务经营者" ，不强制要求到政府注册。即便如此，保护通信隐私的合法性仍强制实行。作为一个结论，如果你在日本领土运营 VPN Gate 服务，你不能泄露经由你操作的 VPN Gate 服务传送的通讯秘密。

5.11. VPN Gate 客户端
如果 SoftEther VPN 客户端包含 VPN Gate 客户端插件，你可以在互联网上用它来获得当前操作的 VPN Gate 服务的服务器列表，使一个 VPN 连接到列表上的特定服务器。
VPN Gate 客户端始终定期保持 VPN Gate 服务的最新列表。要小心，如果你使用的是按使用量付费的互联网线路。
当您启动 VPN Gate 客户端软件，要求你激活或不是 VPN Gate 服务的屏幕将出现。VPN Gate 服务的详细信息，请阅读上述各节。

5.12. 在加入或使用 VPN Gate 学术实验项目之前的注意事项
VPN Gate 学术实验服务是作为日本筑波大学研究生院的一个研究项目运营的。该服务受日本法律管理。其他国家的法律不受我们关注也不承担责任。
从本质上讲，在世界上有近 200 个国家，都有不同的法律。不可能在软件发布前去验证每一个国家的法律和法规，并使我们的软件符合所有国家的法律。如果用户在一个特定的国家使用 VPN Gate 服务，损坏公务人员的权力，服务或软件的开发者将永远不会负责恢复或补偿等损害或刑事责任。
通过使用本软件和服务，用户有自己的义务必须遵守所有相关的法律和规则。用户将完全承担任何损失和使用本软件及服务导致的责任，无论日本领土以内还是以外。
如果你不同意也不理解上述警告，不要使用任何 VPN Gate 学术实验服务功能。
VPN Gate 仅仅是学术目的的一个研究项目。VPN Gate 是作为 SoftEtherVPN 和 UT-VPN 的一个插件被开发的。然而， VPN Gate 的每一部分都是在筑波大学的这一研究项目被开发的。VPN Gate 的任何部分都不是 SoftEther 公司开发的。VPN Gate 研究项目不是由 SoftEther 公司引导、经营，推广和保证的。

5.13. VPN Gate 客户端的 P2P 中继功能可加强针对防火墙管控的规避能力
P2P 中继功能是为了加强规避防火墙管控的能力。如果 P2P 中继功能在您的 VPN Gate 客户端被启用，那么 P2P 中继功能将接受来自 VPN Gate 用户的 VPN 连接，提供中继功能给外部远程 VPN Gate 的服务器，这是由第三方在免费的互联网环境下托管的。此 P2P 中继功能从来不提供共享 NAT 功能，也不更换 VPN Gate 用户的传出 IP 地址为你的 IP 地址，因为这个 P2P 中继功能只提供 "反射服务" (发夹中继) ，从进入的 VPN Gate 用户中继到一个外部的 VPN Gate 服务器。在这种情况下，经由您的 P2P 中继功能的 VPN 隧道将终止于外部的 VPN Gate 服务器，而不是你的 VPN Gate 客户端。然而， VPN Gate 服务器作为最终目的地将记录您的 IP 地址作为通过您的 P2P 中继功能发起的 VPN 隧道的源 IP 地址。此外，经由你的 P2P 中继功能传输的用户数据包将被记录在您的计算机的数据包日志上，如 5.8 章所述。当您安装了 VPN Gate 客户端之后，如果将 P2P 中继功能设置为自动启用，那么在 5.2，5.3，5.4，5.5，5.6，5.7，5.8，5.9，5.10，5.11 和 5.12 章节中的所有事项将被应用于你的电脑，与您启用 VPN Gate 服务 (VPN Gate 服务器功能) 时的情况相同。如果你的 P2P 功能被启用，那么在第 5.5 章节中描述的您的计算机 IP 地址和默认运营商名字将被列在由 VPN Gate 项目提供的 VPN Gate 服务器列表上。您可以通过手动编辑 "vpn_gate_relay.config" 文件更改这些字符串。需要注意的是，在编辑之前您需要停止 VPN 客户端服务。如果 VPN Gate 客户端检测到您的计算机位于存在审查制度的防火墙区域， VPN 客户端会自动启用您的计算机上的 P2P 中继功能。如果您希望禁用 P2P 中继功能，您必须在 VPN 客户端的配置文件 "vpn_client.config" 上设置 "DisableRelayServer" 标志为 "true" 。需要注意的是，编辑它之前您需要停止 VPN 客户端服务。即使您的国家或地区有法律限制运行 P2P 中继功能， VPN Gate 客户端仍会激活 P2P 中继功能。如果您身处于存在这些法律限制的区域，请您遵守相关法律法规，通过设置 "DisableRelayServer" 标志手动禁用 VPN Gate 客户端的 P2P 中继功能。


