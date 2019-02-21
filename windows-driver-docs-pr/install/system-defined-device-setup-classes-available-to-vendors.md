---
title: 向供应商提供的系统定义的设备安装程序类
description: 向供应商提供的系统定义的设备安装程序类
ms.assetid: d4b8a964-f843-4960-9077-46746af27a61
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5debac8428ea3bb252f02a2ab0178ff96fea6b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521330"
---
# <a name="system-defined-device-setup-classes-available-to-vendors"></a>向供应商提供的系统定义的设备安装程序类  
  
  
由操作系统定义的以下类和 Guid。 除非另有说明，这些类和 Guid 可用于安装的设备 （或驱动程序） 在 Windows 2000 和更高版本的 Windows 上：  
  
**电池设备**  
类 = 电池  
ClassGuid = {72631e54-78a4-11d0-bcf7-00aa00b7b32a}  
此类包括电池设备和 UPS 设备。  
  
**生物识别设备**  
类 = 生物识别  
ClassGuid = {53D29EF7-377C-4D14-864B-EB3A85769359}  
（Windows Server 2003 和更高版本的 Windows）此类包括所有基于生物识别的个人识别设备。  
  
**蓝牙设备**  
类 = 蓝牙  
ClassGuid = {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}  
（Windows XP SP1 和更高版本的 Windows）此类包括所有蓝牙设备。  
  
**照相机设备**  
类 = 照相机  
ClassGuid = {ca3e7ab9-b4c3-4ae6-8251-579ef933890f}  
（Windows 10 版本 1709年及更高版本的 Windows）此类包括通用照相机的驱动程序。  
  
**CD-ROM 驱动器**  
类 = CDROM  
ClassGuid = {4d36e965-e325-11ce-bfc1-08002be10318}  
此类包括 CD-ROM 驱动器，包括 SCSI CD-ROM 驱动器。 默认情况下，系统的 CD-ROM 类安装程序还将安装的系统提供 CD 的音频驱动程序和 CD-ROM 更换器驱动程序作为插筛选器。  
  
<a href="" id="disk-drives-"></a>**磁盘驱动器**  
类 = 磁盘驱动器  
ClassGuid = {4d36e967-e325-11ce-bfc1-08002be10318}  
此类包括硬盘驱动器。 另请参阅 HDC 和 SCSIAdapter 类。  
  
**显示适配器**  
类 = 显示  
ClassGuid = {4d36e968-e325-11ce-bfc1-08002be10318}  
此类包括视频适配器。 此类的驱动程序包括显示器驱动程序和视频的微型端口驱动程序。  
  
**扩展 INF**  
类 = 扩展  
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}  
（Windows 10 和更高版本的 Windows）此类包含需要自定义项的所有设备。 有关更多详细信息，请参阅[使用扩展 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)。  
  
<a href="" id="floppy-disk-controllers-"></a>**软盘控制器**  
类 = FDC  
ClassGuid = {4d36e969-e325-11ce-bfc1-08002be10318}  
此类包括软盘驱动器控制器。  
  
**软盘驱动器**  
类 = 软盘上  
ClassGuid= {4d36e980-e325-11ce-bfc1-08002be10318}  
此类包括软盘驱动器。  
  
<a href="" id="hard-disk-controllers-"></a>**硬盘控制器**  
类 = HDC  
ClassGuid = {4d36e96a-e325-11ce-bfc1-08002be10318}  
此类包括硬盘控制器，包括 ATA/ATAPI 控制器，但不是 SCSI 和 RAID 磁盘控制器。  
  
**人机接口设备 (HID)**  
类 = HIDClass  
ClassGuid = {745a17a0-74d3-11d0-b6fe-00a0c90f57da}  
此类包含交互式输入的设备，由系统提供运营[HID 类驱动程序](https://msdn.microsoft.com/library/windows/hardware/jj126193)。 这包括 USB 设备是否符合[USB HID 标准](../hid/hid-over-usb.md)和使用 HID 微型驱动程序的非 USB 设备。 有关详细信息，请参阅[HIDClass 设备安装程序类](../hid/minidriver-operations.md)。 （请参阅此列表中更高版本的键盘或鼠标类。）  
  
**IEEE 1284.4 设备**  
类 = Dot4  
ClassGuid = {48721b56-6795-11d2-b1a8-0080c72e74a2}  
此类包括控制操作的多功能 IEEE 1284.4 外围设备的设备。  
  
**IEEE 1284.4 打印函数**  
类 = Dot4Print  
ClassGuid = {49ce6ac8-6f86-11d2-b1e5-0080c72e74a2}  
此类包括 Dot4 打印功能。 Dot4 打印功能是 Dot4 设备上的函数，并具有单个子设备是打印机设备安装程序类的成员。  
  
**支持 61883 协议的 IEEE 1394 设备**  
类 = 61883  
ClassGuid = {7ebefbc0-3200-11d2-b4c2-00a0C9697d07}  
此类包括支持 IEC 61883 协议设备类的 IEEE 1394 设备。  
  
61883 组件包括*是 61883.sys* 1394年总线通过将传输音频和视频数据的各种流的协议驱动程序。 当前，其中包括标准/高/低质量 DV、 MPEG2、 DSS 和音频。 这些数据流由 IEC 61883 规范定义。  
  
**支持 AVC 协议的 IEEE 1394 设备**  
类 = AVC  
ClassGuid = {c06ff265-ae09-48f0-812c-16753d7cba83}  
此类包括支持 AVC 协议设备类的 IEEE 1394 设备。  
  
**支持 SBP2 协议的 IEEE 1394 设备**  
类 = SBP2  
ClassGuid = {d48179be-ec20-11d1-b6b8-00c04fa372a7}  
此类包括支持 SBP2 协议设备类的 IEEE 1394 设备。  
  
<a href="" id="ieee-1394-host-bus-controller-"></a>**IEEE 1394 主机总线控制器**  
类 = 1394年  
ClassGuid = {6bdd1fc1-810f-11d0-bec7-08002be2092f}  
此类包括连接 PCI 总线，但不是 1394年外围设备上的 1394年主控制器。 此类的驱动程序是系统提供。  
  
<a href="" id="imaging-device-"></a>**图像处理设备**  
类 = 图像  
ClassGuid = {6bdd1fc6-810f-11d0-bec7-08002be2092f}  
此类包括静止图像捕获设备、 数字照相机和扫描仪。  
  
**IrDA 设备**  
类 = 红外  
ClassGuid = {6bdd1fc5-810f-11d0-bec7-08002be2092f}  
此类包括红外设备。 此类的驱动程序包括序列红外线 （ir） 和快速 IR NDIS 微型端口，但另请参阅其他 NDIS 网络适配器微型端口的网络适配器类。  
  
**键盘**  
类 = 键盘  
ClassGuid = {4d36e96b-e325-11ce-bfc1-08002be10318}  
此类包括所有键盘。 也就是说，它还必须指定枚举的子 HID 键盘设备 （辅助） INF 中。  
  
**媒体更换器**  
类 = MediumChanger  
ClassGuid = {ce5939ae-ebde-11d0-b181-0000f8753ec4}  
此类包括 SCSI 媒体更换器设备。  
  
<a href="" id="memory-technology-driver-"></a>**内存技术驱动程序**  
类 = MTD  
ClassGuid = {4d36e970-e325-11ce-bfc1-08002be10318}  
此类包括内存设备，如闪存卡。  
  
<a href="" id="modem-"></a>**调制解调器**  
类 = 调制解调器  
ClassGuid = {4d36e96d-e325-11ce-bfc1-08002be10318}  
此类包括调制解调器设备或*软件调制解调器*。 这些设备拆分调制解调器设备和设备驱动程序之间的功能。 有关调制解调器 INF 文件和 Microsoft Windows 驱动程序模型 (WDM) 调制解调器设备的详细信息，请参阅[调制解调器 INF 文件的概述](https://msdn.microsoft.com/library/windows/hardware/ff542559)并[添加 WDM 调制解调器支持](https://msdn.microsoft.com/library/windows/hardware/ff541218)。  
  
<a href="" id="monitor-"></a>**监视器**  
类 = 监视器  
ClassGuid = {4d36e96e-e325-11ce-bfc1-08002be10318}  
此类包括显示监视器。 此类设备 INF 不安装任何设备驱动程序，但改为指定的特定监视器的视频适配器的驱动程序存储在注册表中供使用的功能。 （监视器枚举作为显示适配器的子设备。）  
  
<a href="" id="mouse-"></a>**鼠标**  
类 = 鼠标  
ClassGuid = {4d36e96f-e325-11ce-bfc1-08002be10318}  
此类包括所有鼠标设备和其他类型的指针设备，如轨迹。 也就是说，此类还必须枚举的子 HID 鼠标设备 （辅助） INF 中指定。  
  
**多功能设备**  
类 = 多功能  
ClassGuid = {4d36e971-e325-11ce-bfc1-08002be10318}  
此类包括组合卡，如 PCMCIA 调制解调器和网卡适配器。 这样的插多功能设备的驱动程序安装在此类，并为其子设备单独枚举的调制解调器和网卡。  
  
<a href="" id="multimedia-"></a>**多媒体**  
类 = 媒体  
ClassGuid = {4d36e96c-e325-11ce-bfc1-08002be10318}  
此类包括音频和 DVD 的多媒体设备、 游戏杆端口和全动态视频捕获设备。  
  
**多端口的串行适配器**  
类 = MultiportSerial  
ClassGuid = {50906cb8-ba12-11d1-bf5d-0000f805f530}  
此类包括智能多端口的串行卡，但不是外围设备，它们将连接到其端口。 它不包括多端口流逝串行控制器 （16550 类型） 或单个端口串行控制器 （请参阅端口类）。  
  
<a href="" id="network-adapter-"></a>**网络适配器**  
类 = Net  
ClassGuid = {4d36e972-e325-11ce-bfc1-08002be10318}  
此类包括 NDIS 微型端口驱动程序不包括快速 IR 微型端口驱动程序、 NDIS 中间驱动程序 （的虚拟适配器） 和的 CoNDIS MCM 微型端口驱动程序。  
  
<a href="" id="network-client-"></a>**网络客户端**  
类 = NetClient  
ClassGuid = {4d36e973-e325-11ce-bfc1-08002be10318}  
此类包括网络和/或打印提供商。  
  
**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。  
  
   
  
**网络服务**  
类 = NetService  
ClassGuid = {4d36e974-e325-11ce-bfc1-08002be10318}  
此类包括网络服务，例如重定向程序和服务器。  
  
<a href="" id="network-transport-"></a>**网络传输**  
类 = NetTrans  
ClassGuid = {4d36e975-e325-11ce-bfc1-08002be10318}  
此类包括 NDIS 协议的 CoNDIS 独立调用管理器和 CoNDIS 客户端，除了中的传输堆栈的更高级别驱动程序。  
  
**PCI SSL 加速器**  
类 = SecurityAccelerator  
ClassGuid = {268c95a1-edfe-11d3-95c3-0010dc4050a5}  
此类包含设备，加速安全套接字层 (SSL) 加密处理。  
  
<a href="" id="pcmcia-adapters-"></a>**PCMCIA 适配器**  
类 = PCMCIA  
ClassGuid = {4d36e977-e325-11ce-bfc1-08002be10318}  
此类包括 PCMCIA 和 CardBus 主机控制器，但不是 PCMCIA 或 CardBus 外围设备。 此类的驱动程序是系统提供。  
  
<a href="" id="ports--com---lpt-ports--"></a>**端口 （COM 和 LPT 端口）**  
类 = 端口  
ClassGuid = {4d36e978-e325-11ce-bfc1-08002be10318}  
此类包含串行和并行端口设备。 另请参阅 MultiportSerial 类。  
  
<a href="" id="printers-"></a>**打印机**  
类 = 打印机  
ClassGuid = {4d36e979-e325-11ce-bfc1-08002be10318}  
此类包括打印机。  
  
**打印机，总线特定类驱动程序**  
类 = PNPPrinters  
ClassGuid = {4658ee7e-f050-11d1-b6bd-00c04fa372a7}  
此类包括 SCSI/1394年枚举打印机。 此类的驱动程序提供特定的总线打印机通信。  
  
<a href="" id="processors-"></a>**处理器**  
类 = 处理器  
ClassGuid = {50127dc3-0f36-415e-a6cc-4cb3be910b65}  
此类包括处理器类型。  
  
<a href="" id="scsi-and-raid-controllers-"></a>**SCSI 和 RAID 控制器**  
类 = SCSIAdapter  
ClassGuid = {4d36e97b-e325-11ce-bfc1-08002be10318}  
此类包括 SCSI Hba （主机总线适配器） 和磁盘阵列控制器。  
  
**传感器**  
类 = 传感器  
ClassGuid = {5175d334-c371-4806-b3ba-71fd53c9258d}  
（Windows 7 和更高版本的 Windows）此类包括传感器和位置设备，例如 GPS 设备。  
  
**智能卡读卡器**  
Class = SmartCardReader  
ClassGuid = {50dd5230-ba8a-11d1-bf5d-0000f805f530}  
此类包括智能卡读卡器。  
  
**软件组件**  
类 = SoftwareComponent  
ClassGuid = {5c4c3332-344d-483c-8739-259e934c9cc8}  
（Windows 10 版本 1703年和更高版本的 Windows）此类包括虚拟子设备来封装软件组件。 有关更多详细信息，请参阅[包含一个 INF 文件添加软件组件](https://docs.microsoft.com/windows-hardware/drivers/install/adding-software-components-with-an-inf-file)。  
  
<a href="" id="storage-volumes-"></a>**存储卷**  
类 = 卷  
ClassGuid = {71a27cdd-812a-11d0-bec7-08002be2092f}  
系统提供的逻辑卷管理器和创建设备对象表示存储卷，如系统磁盘类驱动程序的类驱动程序定义的此类包括存储卷。  
  
<a href="" id="system-devices-"></a>**系统设备**  
类 = 系统  
ClassGuid = {4d36e97d-e325-11ce-bfc1-08002be10318}  
此类包括 Hal、 系统总线、 系统桥、 系统 ACPI 驱动程序和系统卷管理器驱动程序。  
  
<a href="" id="tape-drives-"></a>**磁带驱动器**  
类 = TapeDrive  
ClassGuid = {6d807884-7d21-11cf-801c-08002be10318}  
此类包括磁带驱动器，包括所有磁带 miniclass 驱动程序。  
  
**USB 设备**  
类 = USBDevice  
ClassGuid = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}  
USBDevice 包含不属于另一个类的所有 USB 设备。 此类不用于 USB 主控制器和中心。  
  
**Windows CE USB ActiveSync 设备**  
类 = WCEUSBS  
ClassGuid = {25dbce51-6c8f-4a72-8a6d-b54c2b4fc835}  
此类包括 Windows CE ActiveSync 的设备。  
  
WCEUSBS 安装程序类支持一台个人计算机和通过 USB 与 Windows CE ActiveSync 驱动程序 （通常情况下，PocketPC 设备） 兼容的设备之间的通信。  
  
**Windows 便携设备 (WPD)**  
类 = WPD  
ClassGuid = {eec5ad98-8080-425f-922a-dabf3de3f69a}  
（Windows Vista 和更高版本的 Windows）此类包括 WPD 设备。  
  
**Windows SideShow**  
类 = 边栏显示  
ClassGuid = {997b5d8d-c442-4f2e-baf3-9c8e671e9e21}  
（Windows Vista 和更高版本的 Windows）此类包括与 Windows 边栏显示兼容的所有设备。  
  
   
  
   
  

  
  
  
  
