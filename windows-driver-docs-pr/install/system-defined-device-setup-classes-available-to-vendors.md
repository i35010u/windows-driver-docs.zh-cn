---
title: INF 版本部分的 Class 和 ClassGuid 条目
description: INF 版本部分的 Class 和 ClassGuid 条目
ms.assetid: d4b8a964-f843-4960-9077-46746af27a61
ms.date: 08/27/2020
ms.localizationpriority: medium
ms.custom: contperfq1
ms.openlocfilehash: 9c0e48690016f723856f2e8b3856361c62a9be83
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009937"
---
# <a name="class-and-classguid-entries-for-inf-version-section"></a>INF 版本部分的 Class 和 ClassGuid 条目  

如果要为特定设备类别编写 Windows 设备驱动程序，可以使用以下列表来选择正确的预定义值，以用于 `Class` `ClassGuid` 驱动程序 INF 文件的 [版本部分](inf-version-section.md) 中的和条目。

若要查看这些条目在 INF 文件中的显示方式，请查看[Windows 驱动程序示例](https://github.com/microsoft/Windows-driver-samples)存储库中的 " [cdrom](https://github.com/microsoft/Windows-driver-samples/blob/aaeca58c5e7b67740a603a3150db225670b42bb6/storage/class/cdrom/src/cdrom.inf#L7-L8) "。

除非特别指出，列表中的值可用于在 Windows 2000 和更高版本上安装设备驱动程序。

> [!NOTE]
> 如果你正在寻找有关排查 CD 或 DVD 驱动器问题的信息，请参阅 [cd 驱动器或 dvd 驱动器无法按预期工作](https://support.microsoft.com/help/929461/the-cd-drive-or-the-dvd-drive-does-not-work-as-expected-on-a-computer)。

## <a name="device-categories-and-class-values"></a>设备类别和类值 

**电池设备**  
类 = 电池  
ClassGuid = {72631e54-78a4-11d0-bcf7-00aa00b7b32a}  
此类包括电池设备和 UPS 设备。  
  
**生物识别设备**  
类 = 生物识别  
ClassGuid = {53D29EF7-377C-4D14-864B-EB3A85769359}  
 (Windows Server 2003 及更高版本的 Windows) 此类包括所有基于生物识别的个人标识设备。  
  
**蓝牙设备**  
类 = 蓝牙  
ClassGuid = {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}  
 (Windows XP SP1 及更高版本的 Windows) 此类包括所有蓝牙设备。  
  
**照相机设备**  
类 = 相机  
ClassGuid = {ca3e7ab9-b4c3-4ae6-8251-579ef933890f}  
 (Windows 10 1709 版及更高版本的 Windows) 此类包含通用照相机驱动程序。  
  
**Cd-rom 驱动器**  
类 = CDROM  
ClassGuid = {4d36e965-e325-11ce-bfc1-08002be10318}  
此类包含 cd-rom 驱动器，其中包括 SCSI cd-rom 驱动器。 默认情况下，系统的 CD-ROM 类安装程序还会安装系统提供的 CD 音频驱动程序和 CD-ROM 更换器驱动程序作为即插即用筛选器。  
  
<a href="" id="disk-drives-"></a>**磁盘驱动器**  
类 = DiskDrive  
ClassGuid = {4d36e967-e325-11ce-bfc1-08002be10318}  
此类包括硬盘驱动器。 另请参阅 HDC 和 SCSIAdapter 类。  
  
**显示适配器**  
类 = 显示  
ClassGuid = {4d36e968-e325-11ce-bfc1-08002be10318}  
此类包含视频适配器。 此类的驱动程序包括显示器驱动程序和视频微型端口驱动程序。  
  
**扩展 INF**  
类 = 扩展  
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}  
 (Windows 10 及更高版本的 Windows) 此类包括需要自定义的所有设备。 有关更多详细信息，请参阅 [使用扩展 INF 文件](./using-an-extension-inf-file.md)。  
  
<a href="" id="floppy-disk-controllers-"></a>**软盘控制器**  
类 = FDC  
ClassGuid = {4d36e969-e325-11ce-bfc1-08002be10318}  
此类包含软盘驱动器控制器。  
  
**软盘驱动器**  
类 = FloppyDisk  
ClassGuid = {4d36e980-e325-11ce-bfc1-08002be10318}  
此类包含软盘驱动器。  
  
<a href="" id="hard-disk-controllers-"></a>**硬盘控制器**  
类 = HDC  
ClassGuid = {4d36e96a-e325-11ce-bfc1-08002be10318}  
此类包括硬盘控制器（包括 ATA/ATAPI 控制器），但不包括 SCSI 和 RAID 磁盘控制器。  
  
**人体学接口设备 (HID) **  
类 = HIDClass  
ClassGuid = {745a17a0-74d3-11d0-b6fe-00a0c90f57da}  
此类包括由系统提供的 [HID 类驱动程序](/previous-versions/jj126193(v=vs.85))操作的交互式输入设备。 这包括符合使用 HID 微型驱动程序的 [USB HID 标准](../hid/hid-over-usb.md) 和非 usb 设备的 usb 设备。 有关详细信息，请参阅 [HIDClass 设备安装程序类](../hid/minidriver-operations.md)。  (另请参阅此列表后面的键盘或鼠标类。 )   
  
**IEEE 1284.4 设备**  
类 = Dot4  
ClassGuid = {48721b56-6795-11d2-b1a8-0080c72e74a2}  
此类包括控制多功能 IEEE 1284.4 外围设备的操作的设备。  
  
**IEEE 1284.4 打印功能**  
类 = Dot4Print  
ClassGuid = {49ce6ac8-6f86-11d2-b1e5-0080c72e74a2}  
此类包括 Dot4 打印功能。 Dot4 打印功能是 Dot4 设备上的一个函数，并且有一个子设备，该设备是打印机设备安装程序类的成员。  
  
**支持61883协议的 IEEE 1394 设备**  
类 = 61883  
ClassGuid = {7ebefbc0-3200-11d2-b4c2-00a0C9697d07}  
此类包括支持 IEC-61883 协议设备类的 IEEE 1394 设备。  
  
61883组件包含通过1394总线传输各种音频和视频数据流的 *61883.sys* 协议驱动程序。 目前包括标准/高/低质量 DV、MPEG2、DSS 和音频。 这些数据流由 IEC-61883 规范定义。  
  
**支持 AVC 协议的 IEEE 1394 设备**  
类 = AVC  
ClassGuid = {c06ff265-ae09-48f0-812c-16753d7cba83}  
此类包括支持 AVC 协议设备类的 IEEE 1394 设备。  
  
**支持 SBP2 协议的 IEEE 1394 设备**  
类 = SBP2  
ClassGuid = {d48179be-ec20-11d1-b6b8-00c04fa372a7}  
此类包括支持 SBP2 协议设备类的 IEEE 1394 设备。  
  
<a href="" id="ieee-1394-host-bus-controller-"></a>**IEEE 1394 主机总线控制器**  
类 = 1394  
ClassGuid = {6bdd1fc1-810f-11d0-bec7-08002be2092f}  
此类包括在 PCI 总线上连接的1394主机控制器，但不包括1394外设。 此类的驱动程序是系统提供的。  
  
<a href="" id="imaging-device-"></a>**成像设备**  
类 = 映像  
ClassGuid = {6bdd1fc6-810f-11d0-bec7-08002be2092f}  
此类包括静止图像捕获设备、数码相机和扫描仪。  
  
**IrDA 设备**  
类 = 红外  
ClassGuid = {6bdd1fc5-810f-11d0-bec7-08002be2092f}  
此类包括红外设备。 此类的驱动程序包括串行 IR 和快速 IR NDIS 微型端口，但另请参阅其他 NDIS 网络适配器微型端口的网络适配器类。  
  
**键盘**  
类 = 键盘  
ClassGuid = {4d36e96b-e325-11ce-bfc1-08002be10318}  
此类包括所有键盘。 也就是说，还必须在枚举的子 HID 键盘设备 (辅助) INF 中指定它。  
  
**媒体转换器**  
类 = MediumChanger  
ClassGuid = {ce5939ae-ebde-11d0-b181-0000f8753ec4}  
此类包括 SCSI 媒体转换器设备。  
  
<a href="" id="memory-technology-driver-"></a>**内存技术驱动程序**  
类 = MTD  
ClassGuid = {4d36e970-e325-11ce-bfc1-08002be10318}  
此类包括内存设备，如闪存卡。  
  
<a href="" id="modem-"></a>**R**  
类 = 调制解调器  
ClassGuid = {4d36e96d-e325-11ce-bfc1-08002be10318}  
此类包括调制解调器设备或 *软件调制解调器*。 这些设备会在调制解调器设备和设备驱动程序之间拆分功能。 有关调制解调器 INF 文件和 Microsoft Windows 驱动模型 (WDM) 调制解调器设备的详细信息，请参阅 [调制解调器 Inf 文件概述](/previous-versions/windows/hardware/modem/ff542559(v=vs.85)) 和 [添加 WDM 调制解调器支持](/previous-versions/windows/hardware/modem/ff541218(v=vs.85))。  
  
<a href="" id="monitor-"></a>**监控器**  
类 = 监视器  
ClassGuid = {4d36e96e-e325-11ce-bfc1-08002be10318}  
此类包括显示器。 此类设备的 INF 不 (s) 安装设备驱动程序，而是指定要存储在注册表中的特定监视器的功能，以供视频适配器驱动程序使用。  (监视器将被枚举为显示适配器的子设备。 )   
  
<a href="" id="mouse-"></a>**鼠标键**  
类 = 鼠标  
ClassGuid = {4d36e96f-e325-11ce-bfc1-08002be10318}  
此类包括所有鼠标设备和其他类型的指针设备，如 trackballs。 也就是说，还必须在已枚举的子 HID 鼠标设备的 (辅助) INF 中指定此类。  
  
**多功能设备**  
类 = 多功能  
ClassGuid = {4d36e971-e325-11ce-bfc1-08002be10318}  
此类包含组合卡，如 PCMCIA 调制解调器和网卡适配器。 此类即插即用多功能设备的驱动程序安装在此类下，并将调制解调器和网卡分别作为其子设备进行枚举。  
  
<a href="" id="multimedia-"></a>**媒体**  
类 = 媒体  
ClassGuid = {4d36e96c-e325-11ce-bfc1-08002be10318}  
此类包括音频和 DVD 多媒体设备、游戏杆端口和全运动视频捕获设备。  
  
**多端口串行适配器**  
类 = MultiportSerial  
ClassGuid = {50906cb8-ba12-11d1-bf5d-0000f805f530}  
此类包括智能多端口串行卡，但不包括连接到其端口的外围设备。 它不包括 unintelligent (16550) 多端口串行控制器或单端口串行控制器 (参阅 port 类) 。  
  
<a href="" id="network-adapter-"></a>**网络适配器**  
类 = Net  
ClassGuid = {4d36e972-e325-11ce-bfc1-08002be10318}  
此类包含网络适配器驱动程序。  这些驱动程序必须调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 或 [**NetAdapterCreate**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)。  不使用 NDIS 或 Get-netadapter 的驱动程序应使用不同的安装程序类。
  
<a href="" id="network-client-"></a>**网络客户端**  
类 = NetClient  
ClassGuid = {4d36e973-e325-11ce-bfc1-08002be10318}  
此类包括网络和/或打印提供程序。  
  
**请注意**，  **NetClient**组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  
  
   
  
**Network Service**  
类 = 空间  
ClassGuid = {4d36e974-e325-11ce-bfc1-08002be10318}  
此类包含网络服务，如重定向器和服务器。  
  
<a href="" id="network-transport-"></a>**网络传输**  
类 = NetTrans  
ClassGuid = {4d36e975-e325-11ce-bfc1-08002be10318}  
除了传输堆栈中的更高级别驱动程序外，此类还包括 CoNDIS 独立调用管理器和 CoNDIS 客户端的 NDIS 协议。  
  
**PCI SSL 加速器**  
类 = SecurityAccelerator  
ClassGuid = {268c95a1-edfe-11d3-95c3-0010dc4050a5}  
此类包括加速安全套接字层 (SSL) 加密处理的设备。  
  
<a href="" id="pcmcia-adapters-"></a>**PCMCIA 适配器**  
类 = PCMCIA  
ClassGuid = {4d36e977-e325-11ce-bfc1-08002be10318}  
此类包括 PCMCIA 和 CardBus 主机控制器，但不包括 PCMCIA 或 CardBus 外设。 此类的驱动程序是系统提供的。  
  
<a href="" id="ports--com---lpt-ports--"></a>**端口 (COM & LPT 端口) **  
类 = 端口  
ClassGuid = {4d36e978-e325-11ce-bfc1-08002be10318}  
此类包括串行和并行端口设备。 另请参阅 MultiportSerial 类。  
  
<a href="" id="printers-"></a>**Printers**  
类 = 打印机  
ClassGuid = {4d36e979-e325-11ce-bfc1-08002be10318}  
此类包含打印机。  
  
**打印机，特定于总线的类驱动程序**  
类 = PNPPrinters  
ClassGuid = {4658ee7e-f050-11d1-b6bd-00c04fa372a7}  
此类包括 SCSI/1394 枚举打印机。 此类的驱动程序为特定总线提供打印机通信。  
  
<a href="" id="processors-"></a>**款**  
类 = 处理器  
ClassGuid = {50127dc3-0f36-415e-a6cc-4cb3be910b65}  
此类包括处理器类型。  
  
<a href="" id="scsi-and-raid-controllers-"></a>**SCSI 和 RAID 控制器**  
类 = SCSIAdapter  
ClassGuid = {4d36e97b-e325-11ce-bfc1-08002be10318}  
此类包括 (主机总线适配器) 和磁盘阵列控制器的 SCSI Hba。  
 
<a href="" id="security-devices-"></a>**安全设备** 类 = Securitydevices  
ClassGuid = {d94ee5d8-d189-4994-83d2-f68d7d41b0e6}  
 (Windows 8.1，Windows 10) 此类包含 [受信任的平台模块](/windows/security/information-protection/tpm/trusted-platform-module-top-node) 芯片。 TPM 是一种安全的加密处理器，可帮助你执行各种操作，如生成、存储和限制加密密钥的使用。 默认情况下，任何新制造设备都必须实现并启用 TPM 2.0。 有关详细信息，请参阅 [TPM 建议](/windows/security/information-protection/tpm/tpm-recommendations)。

**传感器**  
类 = 传感器  
ClassGuid = {5175d334-c371-4806-b3ba-71fd53c9258d}  
 (Windows 7 及更高版本的 Windows) 此类包括传感器和位置设备，如 GPS 设备。  
  
**智能卡读卡器**  
类 = SmartCardReader  
ClassGuid = {50dd5230-ba8a-11d1-bf5d-0000f805f530}  
此类包括智能卡读卡器。  
  
**软件组件**  
类 = SoftwareComponent  
ClassGuid = {5c4c3332-344d-483c-8739-259e934c9cc8}  
 (Windows 10 1703 版及更高版本的 Windows) 此类包括用于封装软件组件的虚拟子设备。 有关更多详细信息，请参阅 [使用 INF 文件添加软件组件](./using-a-component-inf-file.md)。  
  
<a href="" id="storage-volumes-"></a>**存储卷**  
类 = 卷  
ClassGuid = {71a27cdd-812a-11d0-bec7-08002be2092f}  
此类包括由系统提供的逻辑卷管理器和类驱动程序定义的存储卷，它们创建设备对象来表示存储卷，如系统磁盘类驱动程序。  
  
<a href="" id="system-devices-"></a>**系统设备**  
类 = 系统  
ClassGuid = {4d36e97d-e325-11ce-bfc1-08002be10318}  
此类包括 Hal、系统总线、系统桥、系统 ACPI 驱动程序和系统卷管理器驱动程序。  
  
<a href="" id="tape-drives-"></a>**磁带驱动器**  
类 = TapeDrive  
ClassGuid = {6d807884-7d21-11cf-801c-08002be10318}  
此类包括磁带驱动器，包括所有磁带 miniclass 驱动程序。  
  
**USB 设备**  
类 = USBDevice  
ClassGuid = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}  
USBDevice 包括不属于另一类的所有 USB 设备。 此类不用于 USB 主机控制器和中心。  
  
**Windows CE USB ActiveSync 设备**  
类 = WCEUSBS  
ClassGuid = {25dbce51-6c8f-4a72-8a6d-b54c2b4fc835}  
此类包括 Windows CE ActiveSync 设备。  
  
WCEUSBS 安装程序类支持个人计算机与与 Windows CE ActiveSync 驱动程序 (兼容的设备之间的通信。通常，PocketPC 设备通过 USB) 。  
  
**Windows 便携式设备 (WPD) **  
类 = WPD  
ClassGuid = {eec5ad98-8080-425f-922a-dabf3de3f69a}  
 (Windows Vista 及更高版本的 Windows) 此类包括 WPD 设备。  
  
**Windows SideShow**  
类 = 边栏显示  
ClassGuid = {997b5d8d-c442-4f2e-baf3-9c8e671e9e21}  
 (Windows Vista 及更高版本的 Windows) 此类包括与 Windows 边栏显示兼容的所有设备。  
  
   
  
   
  

  
  
  
