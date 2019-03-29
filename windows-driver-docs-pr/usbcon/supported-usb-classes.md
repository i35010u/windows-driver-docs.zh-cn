---
Description: 本主题列出了受支持的 USB 设备类的由 Microsoft 提供的驱动程序。
title: 包含在 Windows 中的 USB 设备类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de0b27f2483509c395b4e685bded1d91f11a936
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419593"
---
# <a name="usb-device-class-drivers-included-in-windows"></a>包含在 Windows 中的 USB 设备类驱动程序

本主题列出了受支持的 USB 设备类的由 Microsoft 提供的驱动程序。

- Microsoft 提供的驱动程序 USB-如果获得批准的设备类。
- 对于复合设备，使用[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)创建物理设备对象 (PDOs) 为每个函数。
- 对于非复合设备或复合设备的一项功能，将[WinUSB (Winusb.sys)](winusb.md)。

**如果您正在安装 USB 驱动程序：** 不需要下载 USB 设备类驱动程序。 它们将自动安装。 在 Windows 中包含这些驱动程序和其安装文件。 在提供了\\Windows\\System32\\DriverStore\\资料库文件夹。 通过 Windows Update 更新驱动程序。

**如果你正在编写自定义驱动程序：** 然后再写入 USB 设备的驱动程序，确定由 Microsoft 提供的驱动程序是否符合设备要求。 如果由 Microsoft 提供的驱动程序不可用于你的设备所属的 USB 设备类，请考虑使用通用驱动程序，Winusb.sys 或 Usbccgp.sys。 编写驱动程序仅在必要时。 中包含多个指导原则[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)。

## <a name="usb-device-classes"></a>USB 设备类

*USB 设备类*是具有类似特征的设备的类别和执行常见的功能。 这些类和其规范定义了 USB 的 IF。 每个设备类由 USB-如果获得批准的类、 子类和协议代码，所有这些由在设备描述符在固件中 IHV 提供。 Microsoft 提供的现成驱动程序用于多个名为这些设备类*USB 设备类驱动程序*。 如果属于受支持的设备类的设备连接到系统中，Windows 会自动加载类驱动程序和设备功能与所需的任何其他驱动程序。

硬件供应商不应编写受支持的设备类的驱动程序。 Windows 类驱动程序可能不支持的所有功能所述的类规范中。 如果设备的功能的一些未实现的类驱动程序，供应商应提供补充类驱动程序来支持整个范围由设备提供的功能与协同工作的驱动程序。

有关 USB 的常规信息-如果获得批准的设备类，请参阅[USB 技术](http://www.usb.org/developers/defined_class/)网站。

有关 USB 类规范和类代码的当前列表，请访问[USB DWG 网站](http://www.usb.org/about/dwg_charter/)。

## <a name="device-setup-classes"></a>设备安装程序类

Windows 对设备进行分类*设备安装程序类*，这表示设备的功能。

Microsoft 定义了适用于大多数设备安装程序类。 Ihv 和 Oem 可以定义新的设备安装程序类，但类仅如果没有，则现有应用。 有关详细信息，请参阅[系统定义设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。

USB 设备的两个重要的设备安装程序类如下所示：

- **USBDevice** {88BAE032-5A81-49f0-BC3D-A4FF138216D6}:对于不属于另一个类的自定义设备，Ihv 必须使用此类。 此类不用于 USB 主控制器和中心。

- **USB** {36fc9e60-c465-11cf-8056-444553540000}:Ihv 必须使用的自定义设备的此类。 这被保留给 USB 主控制器和 USB 集线器。

设备安装程序类是不同于前面所述的 USB 设备类。 例如，音频设备在其描述符中具有该版本的 USB 设备类代码。 当连接到系统时，Windows 将加载 Microsoft 提供的类驱动程序，Usbaudio.sys。 在设备管理器中，显示设备的下是**声音、 视频和游戏控制器**，指示设备安装程序类是媒体。

## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供 USB 设备类的驱动程序

<table>
  <thead>
    <tr>
      <th>USB-如果类代码</th>
      <th>设备安装程序类</th>
      <th>Microsoft 提供的驱动程序和 INF</th>
      <th>Windows 支持</th>
     <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>音频 (01 h)</td>
      <td><strong>媒体</strong></br>
{4d36e96c-e325-11ce-bfc1-08002be10318}</td>
      <td>Usbaudio.sys<p>Wdma\_usb.inf</p></td>
      <td>Windows 10 桌面版（家庭版、专业版、企业版和教育版）</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 通过 Usbaudio.sys 驱动程序为 USB 音频设备类提供支持。 详细信息，请参阅"USBAudio 类系统驱动程序"中<a href="https://msdn.microsoft.com/library/windows/hardware/ff537039">内核模式 WDM 音频组件</a>。 有关 Windows 音频支持的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8751">音频设备技术的 Windows</a>网站。</td>
    </tr>
    <tr>
      <td rowspan="4">通信和 CDC 控制 (02 h)</td>
        <tr>
        <td><strong>端口</strong></br>{4D36E978-E325-11CE-BFC1-08002BE10318}</td>
        <td>Usbser.sys</br>Usbser.inf</td>
        <td>Windows 10 桌面版</br>Windows 10 移动版</td>
        <td>在 Windows 10 中，新 INF，Usbser.inf，增添了加载 Usbser.sys 自动为功能驱动程序。<p>有关详细信息，请参阅<a href="usb-driver-installation-based-on-compatible-ids.md">USB 串行驱动程序 (Usbser.sys)</a></p></td>
      </tr>
      <tr>
        <td><strong>调制解调器</strong></br>{4D36E96D-E325-11CE-BFC1-08002BE10318}<p>
        <strong>请注意</strong>支持子类 02 h (ACM)</td>
        <td>Usbser.sys</br>引用 mdmcpq.inf 自定义 INF</td>
        <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>在 Windows 8.1 和早期版本中，Usbser.sys 不自动加载。 若要加载的驱动程序，需要编写它引用调制解调器 INF (mdmcpq.inf) 并包含 INF\[安装\]并\[需要\]部分。<p>从 Windows Vista 开始，你可以启用 CDC，无线移动 CDC (WMCDC) 支持通过设置注册表值，如中所述<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md">支持无线移动通信设备类</a>。<p>启用 CDC 的支持后， <a href="usb-common-class-generic-parent-driver.md">USB 常见类通用父驱动程序</a>枚举与 CDC 和 WMCDC 控件模型相对应的接口集合，并将物理设备对象 (PDO) 分配给这些集合。</td>
      </tr>
      <tr>
        <td><strong>Net</strong></br>{4d36e972-e325-11ce-bfc1-08002be10318}</br><strong>请注意</strong>支持子类 0Eh (MBIM)</td>
        <td>wmbclass.sys</br>Netwmbclass.inf</td>
        <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</td>
        <td>从 Windows 8 开始，Microsoft 提供的 wmbclass.sys 驱动程序，移动宽带设备。 查看，请<a href="https://msdn.microsoft.com/library/windows/hardware/dn265427">MB 接口模型</a>。
</td>
      </tr>
      <tr>
        <td>HID （人机接口设备） (03 h)</td>
        <td><strong>HIDClass</strong></br>{745a17a0-74d3-11d0-b6fe-00a0c90f57da}</td>
        <td>Hidclass.sys</br>Hidusb.sys</br>Input.inf</td>
        <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Microsoft 提供的 HID 类驱动程序 (Hidclass.sys) 和 miniclass 驱动程序 (Hidusb.sys) 运行符合的设备<a href="https://go.microsoft.com/fwlink/p/?LinkId=761243">USB HID 标准</a>。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/jj126193">HID 体系结构</a>并<a href="https://msdn.microsoft.com/library/windows/hardware/jj131708">微型驱动程序和 HID 类驱动程序</a>。 有关输入硬件的 Windows 支持的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8709">输入和 HID-体系结构和驱动程序支持</a>网站。</td>
      </tr>
      <tr>
        <td>物理 (05 h)</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a>
</td>
      </tr>
    <tr>
      <td>图像 (06 h)</td>
      <td><strong>Image</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbscan.sys</br>Sti.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供了管理 Windows XP 和更高版本操作系统的 USB 数字照相机和扫描仪的 Usbscan.sys 驱动程序。 此驱动程序实现了 USB 组件的 Windows 映像体系结构 (WIA)。 有关 WIA 的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff553346">Windows 图像采集驱动程序</a>并<a href="https://go.microsoft.com/fwlink/p/?linkid=8768">Windows Imaging Component</a>网站。 Usbscan.sys WIA 中所扮演的角色的说明，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff550215">WIA 核心组件</a>。</td>
    </tr>
    <tr>
      <td>打印机 (07 h)</td>
      <td><strong>USB</strong><p><strong>请注意</strong>   Usbprint.sys 枚举打印机设备在设备设置类：<strong>打印机</strong><p> {4d36e979-e325-11ce-bfc1-08002be10318}.</td>
      <td>Usbprint.sys</br>Usbprint.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供了管理 USB 打印机的 Usbprint.sys 类驱动程序。 有关 Windows 中的打印机类实现的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8764">打印-体系结构和驱动程序支持</a>网站。</td>
    </tr>
    <tr>
      <td rowspan="3">大容量存储 (08 h)</td>
        <tr>
          <td><strong>USB</strong></td>
          <td>Usbstor.sys</td>
          <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft 提供了 Usbstor.sys 端口驱动程序来管理与 Microsoft 的本机存储类驱动程序的 USB 大容量存储设备。 此驱动程序管理的示例设备堆栈，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff552547">USB 大容量存储设备的设备对象示例</a>。 有关 Windows 存储支持的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8766">存储技术</a>网站。</td>
        </tr>
        <tr>
         <td><strong>SCSIAdapter</strong><p>{4d36e97b-e325-11ce-bfc1-08002be10318}</td>
         <td>子类 (06) 和协议 (62)</br>Uaspstor.sys</br>Uaspstor.inf</td>
         <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</td>
         <td>Uaspstor.sys 是支持大容量流终结点的 SuperSpeed USB 设备的类驱动程序。 有关详细信息，请参阅： <ul>
           <li><a href="https://msdn.microsoft.com/library/windows/hardware/gg585600.aspx">作为类驱动程序在 xHCI 上加载 UASP 存储驱动程序</a></li><li><a href="https://msdn.microsoft.com/library/windows/hardware/jj248714.aspx">针对 Windows 8 的 USB Attached SCSI (UAS) 最佳实践</li></ul></td>
        </tr>
    </tr>
    <tr>
      <td rowspan="3">中心 (09 h)</td>
      <td rowspan="3"><strong>USB</strong><p>{36fc9e60-c465-11cf-8056-444553540000}</td>
      <tr>
      <td>Usbhub.sys</br>Usb.inf</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供用于管理 USB 集线器 Usbhub.sys 驱动程序。 有关集线器类驱动程序和 USB 堆栈之间的关系的详细信息，请参阅<a href="usb-3-0-driver-stack-architecture.md">USB 宿主端驱动程序在 Windows 中的</a>。
        </td>
      <tr>
      <td>Usbhub3.sys</br>Usbhub3.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</td>
      <td>Microsoft 提供 Usbhub3.sys 驱动程序用于管理 SuperSpeed (USB 3.0) USB 集线器。<p>SuperSpeed 集线器附加到 xHCI 控制器时加载驱动程序。 请参阅<a href="usb-3-0-driver-stack-architecture.md">USB 宿主端驱动程序在 Windows 中的</a>。</td>
        </tr>
      </tr>
    </tr>
     <tr>
      <td>CDC 数据 (0Ah)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td rowspan="3">智能卡 (0Bh)</td>
      <td rowspan="3"><strong>SmartCardReader</strong><p>{50dd5230-ba8a-11d1-bf5d-0000f805f530}</td>
        <tr>
          <td>Usbccid.sys （已过时）</td>
          <td>Windows 10 桌面版</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft 提供了 Usbccid.sys 最小化的类驱动程序来管理 USB 智能卡读卡器。 有关 Windows 中的智能卡驱动程序的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff549003">智能卡设计指南</a>。
          <p>请注意，对于 Windows Server 2003、 Windows XP 和 Windows 2000，特殊说明所需的加载该驱动程序，因为它可能已释放晚于操作系统。<p>
          <strong>请注意</strong>UMDF 驱动程序，WUDFUsbccidDriver.dll 替换为 Usbccid.sys 驱动程序。</td>
          </tr>
         <tr>
           <td>WUDFUsbccidDriver.dll</br>WUDFUsbccidDriver.inf</td>
           <td>Windows 8.1</br>Windows 8</td>
           <td>WUDFUsbccidDriver.dll 是 USB CCID 智能卡读卡器设备的用户模式驱动程序。</td>
         </tr>
       </tr>
       <tr>
      <td>内容安全 (0Dh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>建议的驱动程序：<a href="usb-common-class-generic-parent-driver.md">USB 泛型父驱动程序 (Usbccgp.sys)</a>。 某些内容的安全性功能是在 Usbccgp.sys 实现的。 请参阅<a href="content-security-features-in-the-composite-client-generic-parent-drive.md">内容 Usbccgp.sys 中的安全功能</a>。</td>
        </tr>
    </tr>
     <tr>
      <td>视频 (0Eh)</td>
      <td><strong>Image</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbvideo.sys<p>
Usbvideo.inf</td>
      <td>Windows 10 桌面版<p>Windows Vista</td>
      <td>Microsoft 提供 USB 视频类支持通过 Usbvideo.sys 驱动程序。 详细信息，请参阅"USB 视频类驱动程序"下<a href="https://msdn.microsoft.com/library/windows/hardware/ff554228">AVStream 微型驱动程序</a>。
      <p>请注意，对于 Windows XP，特殊说明所需的加载该驱动程序，因为它可能已释放比操作系统的更高版本。</td>
    </tr>
     <tr>
      <td>个人医疗保健 (0Fh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
     </tr>
     <tr>
      <td>音频/视频设备 (10 个 h)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>     <tr>
      <td>诊断设备 (DCh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>     <tr>
      <td>无线控制器 (E0h) <p><strong>请注意</strong>  支持子类 01 h 和协议 01 h</td>
      <td>蓝牙<p>{e0cbf06c-cd8b-4647-bb8a-263b43f0f974}</td>
      <td>Bthusb.sys<p>Bth.inf</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Microsoft 提供了 Bthusb.sys 微型端口驱动程序来管理 USB Bluetooth 无线电收发器。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff536596">蓝牙设计指南</a>。</td>
    </tr>     <tr>
      <td>杂项 (EFh)</td>
      <td><strong>Net</strong><p>
{4d36e972-e325-11ce-bfc1-08002be10318}<p><strong>请注意</strong>  支持子类 04h 和协议 01 h</td>
      <td>Rndismp.sys</br>Rndismp.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>在 Windows Vista 之前支持的 CDC 仅限于 RNDIS 特定于实现的唯一供应商协议使用的控件抽象模型 (ACM) (<strong>bInterfaceProtocol</strong>) 值为 0xFF。 RNDIS 设施中心中的单个类驱动程序，Rndismp.sys 所有 802 样式网卡的管理。 远程 NDIS 的详细讨论，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff569967">远程 NDIS 概述</a>。 Usb 远程 NDIS 的映射是 Usb8023.sys 驱动程序中实现的。 在 Windows 中的网络支持的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8759">网络和无线技术</a>网站。</td>
    </tr>
    <tr>
      <td>特定于应用程序 (FEh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td>特定于供应商设定）</td>
      <td>-</td>
      <td>-</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</td>
      <td>建议的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
  </tbody>
</table>

## <a name="related-topics"></a>相关主题

[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  
