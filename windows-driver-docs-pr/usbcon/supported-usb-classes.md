---
description: 本主题列出了支持的 USB 设备类的 Microsoft 提供的驱动程序。
title: 包含在 Windows 中的 USB 设备类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 70f9bfbdb0a0bc2568a52c97f879e7e4bdeaef6c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107242"
---
# <a name="usb-device-class-drivers-included-in-windows"></a>包含在 Windows 中的 USB 设备类驱动程序

> [!IMPORTANT]
> 本主题面向程序员。 如果你是遇到 USB 问题的客户，请参阅[排除常见 USB 问题](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)

本主题列出了支持的 USB 设备类的 Microsoft 提供的驱动程序。

- USB-IF 批准的设备类的 Microsoft 提供的驱动程序。
- 对于复合设备，请使用 [USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)，为每个函数创建物理设备对象 (PDO)。
- 对于非复合设备或复合设备的函数，请使用 [WinUSB (Winusb.sys)](winusb.md)。

**如果要安装 USB 驱动程序：** 不需要下载 USB 设备类驱动程序。 它们将自动进行安装。 这些驱动程序及其安装文件包含在 Windows 中。 它们在 \\Windows\\System32\\DriverStore\\FileRepository 文件夹中提供。 通过 Windows 更新更新驱动程序。

**如果要编写自定义驱动程序：** 在为 USB 设备编写驱动程序之前，请确定 Microsoft 提供的驱动程序是否满足设备要求。 如果 Microsoft 提供的驱动程序不适用于设备所属的 USB 设备类，请考虑使用通用驱动程序 Winusb.sys 或 Usbccgp.sys。 仅在必要时才编写驱动程序。 有关更多指南信息，请参阅[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)。

## <a name="usb-device-classes"></a>USB 设备类

USB 设备类是具有类似特性并执行常见功能的设备类别  。 这些类及其规范由 USB-IF 定义。 每个设备类都由 USB-IF 批准的类、子类和协议代码标识，所有这些代码都由固件中的设备描述符中的 IHV 提供。 Microsoft 为其中几个设备类（称为 USB 设备类驱动程序）提供内置驱动程序  。 如果属于受支持的设备类的设备连接到系统，则 Windows 将自动加载类驱动程序，并且设备无需其他驱动程序即可运行。

硬件供应商不应为受支持的设备类编写驱动程序。 Windows 类驱动程序可能不支持类规范中描述的所有功能。 如果类驱动程序未实现设备的某些功能，则供应商应提供与类驱动程序配合使用的附属驱动程序，以支持设备提供的全部功能。

有关 USB-IF 批准的设备类的常规信息，请参阅 [USB 技术](https://www.usb.org/developers/defined_class/)网站。

如需获取 USB 类规范和类代码的最新列表，请访问 [USB DWG 网站](https://www.usb.org/about/dwg_charter/)。

## <a name="device-setup-classes"></a>设备安装程序类

Windows 通过指示设备功能设备安装程序类来对设备分类  。

Microsoft 为大多数设备定义安装程序类。 IHV 和 OEM 可以定义新的设备安装程序类，但前提是现有类都不适用。 有关详细信息，请参阅[系统定义的设备安装程序类](/previous-versions/ff553419(v=vs.85))。

USB 设备的两个重要设备安装程序类如下所示：

- **USBDevice** {88BAE032-5A81-49f0-BC3D-A4FF138216D6}：如果自定义设备不属于此类，IHV 必须对这些设备使用另一个类。 此类不用于 USB 主机控制器和集线器。

- **USB** {36fc9e60-c465-11cf-8056-444553540000}：IHV 不得将此类用于其自定义设备。 这是为 USB 主机控制器和 USB 集线器保留的。

设备安装程序类与前面讨论的 USB 设备类不同。 例如，音频设备的描述符中具有 USB 设备类代码 01h。 连接到系统时，Windows 将加载 Microsoft 提供的类驱动程序 Usbaudio.sys。 在“设备管理器”中，设备显示在“声音”、“视频和游戏控制器”下，表示设备安装程序类为“媒体”  。

## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供的 USB 设备类驱动程序

<table>
  <thead>
    <tr>
      <th>USB-IF 类代码</th>
      <th>设备安装程序类</th>
      <th>Microsoft 提供的驱动程序和 INF</th>
      <th>Windows 支持</th>
     <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>音频 (01h)</td>
      <td><strong>媒体</strong></br>
{4d36e96c-e325-11ce-bfc1-08002be10318}</td>
      <td>Usbaudio.sys<p>Wdma\_usb.inf</p></td>
      <td>Windows 10 桌面版（家庭版、专业版、企业版和教育版）</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 通过 Usbaudio.sys 驱动程序为 USB 音频设备类提供支持。 有关详细信息，请参阅<a href="/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components">内核模式 WDM 音频组件</a>中的“USBAudio 类系统驱动程序”。 有关 Windows 音频支持的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=8751">Windows 音频设备技术</a>网站。</td>
    </tr>
    <tr>
      <td rowspan="4">通信和 CDC 控制 (02h)</td>
        <tr>
        <td><strong>端口</strong></br>{4D36E978-E325-11CE-BFC1-08002BE10318}</td>
        <td>Usbser.sys</br>Usbser.inf</td>
        <td>Windows 10 桌面版</br>Windows 10 移动版</td>
        <td>在 Windows 10 中，添加了一个新的 INF (Usbser.inf)，它自动加载 Usbser.sys 作为功能驱动程序。<p>有关详细信息，请参阅 <a href="usb-driver-installation-based-on-compatible-ids.md">USB 串行驱动程序 (Usbser.sys)</a></p></td>
      </tr>
      <tr>
        <td><strong>调制解调器</strong></br>{4D36E96D-E325-11CE-BFC1-08002BE10318}<p>
        <strong>注意</strong> 支持子类 02h (ACM)</td>
        <td>Usbser.sys</br>引用 mdmcpq.inf 的自定义 INF</td>
        <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>在 Windows 8.1 及更低版本中，不会自动加载 Usbser.sys。 若要加载该驱动程序，需要编写引用调制解调器 INF (mdmcpq.inf) 的 INF，并包括 \[Install\] 和 \[Needs\] 部分。<p>从 Windows Vista 开始，可以通过设置注册表值来启用 CDC 和无线移动 CDC (WMCDC) 支持，如<a href="/windows-hardware/drivers/usbcon/support-for-interface-collections">支持无线移动通信设备类</a>中所述。<p>启用 CDC 支持后，<a href="usb-common-class-generic-parent-driver.md">USB 公共类通用父驱动程序</a>枚举对应于 CDC 和 WMCDC 控件模型的接口集合，并将物理设备对象 (PDO) 分配到这些集合。</td>
      </tr>
      <tr>
        <td><strong>Net</strong></br>{4d36e972-e325-11ce-bfc1-08002be10318}</br><strong>注意</strong> 支持子类 0Eh (MBIM)</td>
        <td>wmbclass.sys</br>Netwmbclass.inf</td>
        <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</td>
        <td>从 Windows 8 开始，Microsoft 为移动宽带设备提供 wmbclass.sys 驱动程序。 请参阅 <a href="/windows-hardware/drivers/network/mb-interface-model">MB 接口模型</a>。
</td>
      </tr>
      <tr>
        <td>HID（人机接口设备）(03h)</td>
        <td><strong>HIDClass</strong></br>{745a17a0-74d3-11d0-b6fe-00a0c90f57da}</td>
        <td>Hidclass.sys</br>Hidusb.sys</br>Input.inf</td>
        <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Microsoft 提供 HID 类驱动程序 (Hidclass.sys) 和 miniclass 驱动程序 (Hidusb.sys) 来操作符合 <a href="https://go.microsoft.com/fwlink/p/?LinkId=761243">USB HID 标准</a>的设备。 有关详细信息，请参阅 <a href="/previous-versions/jj126193(v=vs.85)">HID 体系结构</a>和<a href="/windows-hardware/drivers/hid/minidriver-operations">微型驱动程序和 HID 类驱动程序</a>。 有关 Windows 对输入硬件的支持的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8709">输入和 HID - 体系结构和驱动程序支持</a>网站。</td>
      </tr>
      <tr>
        <td>物理 (05h)</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a>
</td>
      </tr>
    <tr>
      <td>图像 (06h)</td>
      <td><strong>映像</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbscan.sys</br>Sti.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供 Usbscan.sys 驱动程序，用于管理 Windows XP 和更高版本的操作系统的 USB 数码相机和扫描仪。 此驱动程序实现 Windows 映像体系结构 (WIA) 的 USB 组件。 有关 WIA 的详细信息，请参阅 <a href="/windows-hardware/drivers/image/windows-image-acquisition-drivers">Windows 图像采集驱动程序</a> 和 <a href="https://go.microsoft.com/fwlink/p/?linkid=8768">Windows 图像处理组件</a>网站。 有关 Usbscan.sys 在 WIA 中扮演的角色的说明，请参阅 <a href="/windows-hardware/drivers/image/wia-core-components">WIA Core 组件</a>。</td>
    </tr>
    <tr>
      <td>打印机 (07h)</td>
      <td><strong>USB</strong><p><strong>注意</strong>   Usbprint.sys 在设备安装程序类下枚举打印机设备：<strong>打印机</strong><p> {4d36e979-e325-11ce-bfc1-08002be10318}.</td>
      <td>Usbprint.sys</br>Usbprint.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供管理 USB 打印机的 Usbprint.sys 类驱动程序。 有关在 Windows 中实现打印机类的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8764">打印 - 体系结构和驱动程序支持</a>网站。</td>
    </tr>
    <tr>
      <td rowspan="3">大容量存储 (08h)</td>
        <tr>
          <td><strong>USB</strong></td>
          <td>Usbstor.sys</td>
          <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft 提供 Usbstor.sys 端口驱动程序，以使用 Microsoft 的本机存储类驱动程序管理 USB 大容量存储设备。 有关由此驱动程序管理的设备堆栈的示例，请参阅 <a href="/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device">USB 大容量存储设备的设备对象示例</a>。 有关 Windows 存储支持的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8766">存储技术</a>网站。</td>
        </tr>
        <tr>
         <td><strong>SCSIAdapter</strong><p>{4d36e97b-e325-11ce-bfc1-08002be10318}</td>
         <td>子类 (06) 和协议 (62)</br>Uaspstor.sys</br>Uaspstor.inf</td>
         <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</td>
         <td>Uaspstor.sys 是支持大容量流终结点的 SuperSpeed USB 设备的类驱动程序。 有关详细信息，请参阅： <ul>
           <li><a href="/previous-versions/windows/hardware/design/dn642103(v=vs.85)">在 xHCI 上将 UASP 存储驱动程序加载为类驱动程序</a></li><li><a href="/previous-versions/windows/hardware/design/dn642113(v=vs.85)">适用于 Windows 8 的 USB 连接 SCSI (UAS) 最佳做法</a></li></ul></td>
        </tr>
    </tr>
    <tr>
      <td rowspan="3">集线器 (09h)</td>
      <td rowspan="3"><strong>USB</strong><p>{36fc9e60-c465-11cf-8056-444553540000}</td>
      <tr>
      <td>Usbhub.sys</br>Usb.inf</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft 提供了用于管理 USB 集线器的 Usbhub.sys 驱动程序。 有关集线器类驱动程序与 USB 堆栈之间的关系的详细信息，请参阅 <a href="usb-3-0-driver-stack-architecture.md">Windows 中的 USB 主机端驱动程序</a>。
        </td>
      <tr>
      <td>Usbhub3.sys</br>Usbhub3.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</td>
      <td>Microsoft 提供用于管理 SuperSpeed (USB 3.0) USB 集线器的 Usbhub3.sys 驱动程序。<p>SuperSpeed 集线器连接到 xHCI 控制器时，将加载驱动程序。 请参阅 <a href="usb-3-0-driver-stack-architecture.md">Windows 中的 USB 主机端驱动程序</a>。</td>
        </tr>
      </tr>
    </tr>
     <tr>
      <td>CDC-Data (0Ah)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td rowspan="3">智能卡 (0Bh)</td>
      <td rowspan="3"><strong>SmartCardReader</strong><p>{50dd5230-ba8a-11d1-bf5d-0000f805f530}</td>
        <tr>
          <td>Usbccid.sys (Obsolete)</td>
          <td>Windows 10 桌面版</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft 提供 Usbccid.sys 迷你类驱动程序来管理 USB 智能卡读卡器。 有关 Windows 中智能卡驱动程序的详细信息，请参阅<a href="/windows-hardware/drivers/smartcard/index">智能卡设计指南</a>。
          <p>请注意，对于 Windows Server 2003、Windows XP 和 Windows 2000，加载此驱动程序需要特别说明，因为它可能晚于操作系统发布。<p>
          <strong>注意</strong> Usbccid.sys 驱动程序已替换为 UMDF 驱动程序 WUDFUsbccidDriver.dll。</td>
          </tr>
         <tr>
           <td>WUDFUsbccidDriver.dll</br>WUDFUsbccidDriver.inf</td>
           <td>Windows 8.1</br>Windows 8</td>
           <td>WUDFUsbccidDriver.dll 是 USB CCID 智能卡读卡器设备的用户模式驱动程序。</td>
         </tr>
       </tr>
       <tr>
      <td>内容安全 (0Dh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推荐的驱动程序：<a href="usb-common-class-generic-parent-driver.md">USB 通用父驱动程序 (Usbccgp.sys)</a>。 某些内容安全功能是在 Usbccgp.sys 中实现的。 请参阅 <a href="content-security-features-in-the-composite-client-generic-parent-drive.md">Usbccgp.sys 中的内容安全功能</a>。</td>
        </tr>
    </tr>
     <tr>
      <td>视频 (0Eh)</td>
      <td><strong>映像</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbvideo.sys<p>
Usbvideo.inf</td>
      <td>Windows 10 桌面版<p>Windows Vista</td>
      <td>Microsoft 通过 Usbvideo.sys 驱动程序提供 USB 视频类支持。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/stream/avstream-minidrivers-design-guide">AVStream 微型驱动程序</a>下的“USB 视频类驱动程序”。
      <p>请注意，对于 Windows Server XP，加载此驱动程序需要特别说明，因为它可能晚于操作系统发布。</td>
    </tr>
     <tr>
      <td>个人保健 (0Fh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
     </tr>
     <tr>
      <td>音频/视频设备 (10h)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>     <tr>
      <td>诊断设备 (DCh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>     <tr>
      <td>无线控制器 (E0h) <p><strong>注意</strong>   支持子类 01h 和协议 01h</td>
      <td>Bluetooth<p>{e0cbf06c-cd8b-4647-bb8a-263b43f0f974}</td>
      <td>Bthusb.sys<p>Bth.inf</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Microsoft 提供 Bthusb.sys 微型端口驱动程序来管理 USB 蓝牙无线电收发器。 有关详细信息，请参阅<a href="/previous-versions/windows/hardware/drivers/ff536596(v=vs.85)">蓝牙设计指南</a>。</td>
    </tr>     <tr>
      <td>杂项 (EFh)</td>
      <td><strong>Net</strong><p>
{4d36e972-e325-11ce-bfc1-08002be10318}<p><strong>注意</strong>   支持子类 04h 和协议 01h</td>
      <td>Rndismp.sys</br>Rndismp.inf</td>
      <td>Windows 10 桌面版</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>在 Windows Vista 之前，对 CDC 的支持仅限于具有供应商唯一协议 (<strong>bInterfaceProtocol</strong>) 值 0xFF 的抽象控制模型 (ACM) 的特定于 RNDIS 的实现。 RNDIS 设备将所有 802 样式的网卡集中在单个类驱动程序 Rndismp.sys 中进行管理。 有关远程 NDIS 的详细讨论，请参阅<a href="/windows-hardware/drivers/network/overview-of-remote-ndis--rndis-">远程 NDIS 概述</a>。 在 Usb8023 驱动程序中实现了远程 NDIS 到 USB 的映射。 有关 Windows 中的网络支持的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=8759">网络和无线技术</a>网站。</td>
    </tr>
    <tr>
      <td>应用程序特定 (FEh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td>供应商特定 (FFh)</td>
      <td>-</td>
      <td>-</td>
      <td>Windows 10 桌面版</br>Windows 10 移动版</td>
      <td>推荐的驱动程序：<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
  </tbody>
</table>

## <a name="related-topics"></a>相关主题

[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)