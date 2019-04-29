---
title: 3D 打印机的自定义 USB 接口支持
description: 本主题介绍如何启用自定义 USB 接口 v3 中的 3D 打印机和 v4 打印驱动程序生态系统。
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1728011ce0dc209c88333bac8a4ab1de81cc781f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324769"
---
# <a name="enable-a-custom-usb-interface-for-a-3d-printer"></a>启用 3D 打印机的自定义 USB 接口

本主题中所述的体系结构支持自定义 USB 接口 3D 打印机 v3 和 v4 打印生态系统中。 标准端口监视器**3dmon.dll**、 转发 3D 打印到 Windows 作业命令**3DPrintService**使用本地服务凭据运行。 该服务将加载并与合作伙伴通信以执行自定义命令的 DLL 所需的 3D 打印作业。 合作伙伴 DLL，并将**3dmon.dll**并**3dprintservice.exe**可再发行组件，安装的设备的 USB 驱动程序包。 合作伙伴 DLL，必须实现并导出的函数与进行通信的一组**3DPrintService**。 在中实现所需的功能与打印后台处理程序服务进行交互的 rest **3dmon.dll**。

> [!NOTE]
> 此体系结构要求的合作伙伴 DLL，为多实例，线程安全。

## <a name="architecture-decisions"></a>体系结构决策

**3DPrintService** windows 服务用于加载和打印的工作流期间调用特定合作伙伴提供的 Dll 中定义的 Api。 这些 Api 将允许与打印机进行通信。

KMDF USB 筛选器驱动程序包在 Windows 更新上发布通过安装即插即用支持 3D 打印机。 KMDF 驱动程序安装合作伙伴软件，并创建一个 3D 打印机设备节点。 使用合作伙伴发布 v4 打印驱动程序从 Windows 更新安装 3D 打印机设备节点。

## <a name="packaging-decisions"></a>打包的决策

### <a name="binaries-and-binary-dependencies"></a>二进制文件和二进制的依赖项

Architectue 使用发布的 Windows 更新上硬件制造商的驱动程序。 此驱动程序包括以下由 Microsoft 提供可再发行组件二进制文件和其依赖项：

- 3dmon.dll
- 3dprintservice.exe
- ms3dprintusb.sys

#### <a name="kernel-mode-usb-filter-driver"></a>内核模式 USB 筛选器驱动程序

KMDF 驱动程序由合作伙伴发布和下图中所示的组件组成。 这与设备硬件 id 相匹配 (通常情况下，VID 和 PID)。 该驱动程序安装这会触发打印队列和切片器驱动程序的安装上创建一个 3D 打印机设备节点。 合作伙伴介绍 v4 打印机驱动程序的 3D 打印机设备节点的创建。

![kmdf usb 筛选器驱动程序](images/kmdf-usb-filter-driver.png)

##### <a name="ms3dprintusbsys"></a>MS3DPrintUSB.sys

创建 3D 打印机开发节点下的枚举的内核模式设备驱动程序\\3DPrint。 通过视频和基于设备节点创建的 Winusb.sys PID 的一个直接匹配项的即插即用子系统通过调用此操作。 驱动程序.inf 文件设置来设置所使用的自定义 DLL **3DPrintService** （如果尚未安装在系统上）。

##### <a name="3dmondll"></a>3dmon.dll

3DMon.dll 是 Microsoft 发布端口监视可再发行组件调用的后台处理程序与 3D 打印机进行通信的二进制文件。

##### <a name="3dprintserviceexe"></a>3dprintservice.exe

3DPrintService.exe 是驱动程序安装过程中作为 Windows 服务安装的 Microsoft 发布的二进制文件。 3DMon 与此服务以执行操作，如打印，bidi，等与 3D 打印机进行通信。

##### <a name="partnerimpldll"></a>Partnerimpl.dll

Partnerimp.dll 是合作伙伴的已发布的 Microsoft 接口实现。 DLL 与使用它们的协议的合作伙伴的设备进行通信。 3DPrintService.exe 加载此 DLL 在运行时来驱动 3D 打印机设备的操作。

![3dprintservice](images/3dprintservice.png)

### <a name="printer-usage-sequence"></a>打印机使用情况序列

- 后台处理程序与 3dmon.dll 将命令发送到 3DPrintService windows 服务进行通信
- 3DPrintService.exe 运行使用 NetworkService 帐户凭据
- 后台处理程序 3dmon.dll，通过将命令发送到 3DPrintService 随时使用 3D 打印机
- 3DPrintService 处理命令，并在合作伙伴提供实现的 Dll 上运行时将调用 Api
- 3DPrintService 移交来自合作伙伴提供的 Dll 的响应返回到后台处理程序

## <a name="interfaces-and-interactions"></a>接口和交互

合作伙伴 DLL 必须导出以下 API 函数：

### <a name="hresult-installin-lpcwstr-args"></a>HRESULT 安装 (\[在\]LPCWSTR args)

此 API 是可选的可以由制造商用来安装自定义软件或为其设备的注册。 例如，安装的设备的驱动程序包中包含建模。 使用系统凭据以启用安装调用此 API。

### <a name="dword-printapisupported"></a>DWORD PrintApiSupported()

第三方制造商使用此 API 以指示 3D 打印服务 API 支持的版本。 下面的 Api 是与版本 1 的 3DPrintService 兼容。

### <a name="hresult-initializeprintlpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT InitializePrint(LPCWSTR pPrinterName, LPCWSTR pPortName, DWORD dwJobId, LPVOID\* ppPartnerData)

在开始初始化打印机的打印事件之前调用此 API。 打印机可以保存 ppPartnerData 参数中的特定作业的状态。 此调用是类似于 StartDocPort 调用。

- **jobId** -用来跟踪作业的作业 id
- **portName** -3D 打印机的端口名
- **printerName** -此打印作业发送到打印机的名称
- **ppPartnerData**的指针到指针，可用于存储作业的任何特定数据

### <a name="hresult-printfilein-dword-jobid-in-lpwstr-portname-in-lpwstr-printername-in-lpwstr-pathtorenderedfileinlpvoid-pppartnerdata"></a>HRESULT PrintFile (\[中\]DWORD jobId\[中\]LPWSTR portName\[中\]LPWSTR printerName\[中\]LPWSTR pathToRenderedFile\[中\]LPVOID\* ppPartnerData)

第三方制造商使用此 API 可在他们的打印机上打印文档。

- **jobId** -用来跟踪作业的作业 id
- **portName** -3D 打印机的端口名
- **printerName** -打印作业发送到打印机的名称
- **pathToRenderedFile** -执行呈现后进行后台处理的文件的位置的 UNC 路径。 第三方制造商处理来自此位置的文件，并在其设备上打印文档
- **ppPartnerData** -指针到指针 InitializePrint API 调用期间存储合作伙伴特定数据安装程序进行寻址。
- **printerName**可从此注册表使用的端口名称。 第三方制造商 maynot 能够使用的端口名与他们的设备进行通信。 打印机名称是唯一的 Windows 计算机上，他们的软件将能够识别哪一台打印机上打印作业。 活动在计算机上的所有打印机都位于以下注册表项：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print\\Printers**

![3d 打印机注册表](images/3d-printer-registry.png)

### <a name="hresult-queryin-lpcwstr-command-in-lpcwstr-commanddata-out-lpwstr-resultbuffer-out-resultbuffersize--in-lpvoid-pppartnerdata"></a>HRESULT 查询 (\_中\_LPCWSTR 命令\_中\_LPCWSTR commandData \_Out\_ LPWSTR resultBuffer\_出\_resultBufferSize，， \_在\_LPVOID\* ppPartnerData)

- **命令**-字符串作为查询发送的命令
- **commandData**的命令参数 （可选）
- **resultBuffer** -的查询参数的调用的结果 >
- **resultBufferSize** -结果缓冲区字符串的大小
- **ppPartnerData** -当前合作伙伴 DLL 实例指针到指针

3Dprint 服务调用合作伙伴 DLL 即可开始的缓冲区大小为命令分配。

分配的内存来保留响应字符串之后, 将再次调用该 DLL 来获取实际的结果。

该 DLL 可以使用从以前的实例数据**IntializePrint()** 调用，以与设备通信而无需每次打开新的通信通道**query （)** 调用函数。

使用此 API 与打印机若要获取设备配置的信息，打印进度，或若要通知的设备的 DLL 中拔出事件的合作伙伴进行通信。

制造商必须支持以下命令：

| Command | CommandData | 输出 | 备注 |
|---------|-------------|--------|----------|
| \\\\Printer.3DPrint:JobStatus | | 作业开始 = {"Status":"确定"} <br> 状态用于完成 {"Status":"已完成"} | 后台处理程序将打印队列 UI 中显示任何返回的值。 这是为了让设备上的打印队列 UI 显示在打印过程的相关信息。 设备可以返回的任意字符串此处 （例如"忙碌"或"完整的 33%"），并且该名称将显示按原义中打印队列作业状态。 |
| \\\\Printer.3DPrint:JobCancel | | {"Status":"已完成"} | 当用户取消打印后台处理程序将调用此命令。 合作伙伴 DLL 时取消操作成功并且已关闭的句柄和线程返回此值。 |
| \\\\Printer.Capabilities:Data | | 符合 PrintDeviceCapabilites (PDC) 架构的 XML 字符串。 | 想要获取有关打印机的详细信息的应用程序调用 PDC 查询。 数据用于描述设备的功能，并可以包含切片器设置，如果该驱动程序依赖于 Microsoft 切片器。 请参阅下面的示例 PDC。 |
| \\\\Printer.3DPrint:Disconnect | | {"Status":"确定"} | 打印机设备的即插即用断开连接时，将触发此查询。 合作伙伴可以用任何所需的操作，例如关闭任何打开的句柄，允许正确重新连接时。 |
| \\\\Printer.3DPrint:Connect | | {"Status":"OK"} | 打印机设备的即插即用连接时，将触发此查询。 合作伙伴可以用任何所需的操作。 |

#### <a name="print-device-capabilities-xml"></a>打印设备功能 XML

以下打印设备功能可以使用 XML 作为示例：

```xml
<?xml version="1.0"?>
<PrintDeviceCapabilities
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    xmlns:psk="http://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="http://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:psk3dx="http://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywords3dextended"
    xmlns:pskv="http://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywordsvendor"
    xmlns:psf="http://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:psf2="http://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    xmlns="http://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    version="2">
    <CapabilitiesChangeID xsi:type="xsd:string">{9F58AF07-DCB6-4865-8CA3-A52EA5DCB05F}</CapabilitiesChangeID>

  <psk3d:Job3DOutputArea psf2:psftype="Property">
    <psk3d:Job3DOutputAreaWidth>150001</psk3d:Job3DOutputAreaWidth>
    <psk3d:Job3DOutputAreaDepth>150001</psk3d:Job3DOutputAreaDepth>
    <psk3d:Job3DOutputAreaHeight>150001</psk3d:Job3DOutputAreaHeight>
  </psk3d:Job3DOutputArea>

  <psk3d:Job3DMaterials psf2:psftype="Property">

      <psk3dx:MaterialPLA>
         <psk:DisplayName>PLA</psk:DisplayName>
         <psk3d:Job3DMaterialType>psk3d:PLA</psk3d:Job3DMaterialType>
         <psk3d:MaterialColor>#FFFFFFFF</psk3d:MaterialColor>

         <psk3dx:platformtemperature>0</psk3dx:platformtemperature>
         <psk3dx:filamentdiameter>1750</psk3dx:filamentdiameter>
         <psk3dx:filamentcalibrationoverride>1.0</psk3dx:filamentcalibrationoverride>
         <psk3dx:extrudertemperature>207</psk3dx:extrudertemperature>

         <psk3dx:SpeedFactor>1.0</psk3dx:SpeedFactor>

         <psk3dx:SetupCommands>
            <!-- Executed during pre-commands: nozzle pre-heating, priming, etc -->
            <psk3dx:command>M104 S207 T1</psk3dx:command>
            <psk3dx:command>M140 S50</psk3dx:command>
         </psk3dx:SetupCommands>

         <psk3dx:SelectCommands>
            <!-- Executed during printing: T0/T1 selection, nozzle wiping sequence,turn fan on/off/gradual, retract the material, temperature, etc-->
            <psk3dx:command>; PLA on</psk3dx:command>
            <psk3dx:command>M108 T1</psk3dx:command>
         </psk3dx:SelectCommands>

         <psk3dx:DeselectCommands>
            <!-- Executed during printing: retract the material, park the nozzle, reduce temperature, etc -->
            <psk3dx:command>; PLA off</psk3dx:command>
         </psk3dx:DeselectCommands>


      </psk3dx:MaterialPLA>
  </psk3d:Job3DMaterials>

  <psk3dx:customStatus>Slicing</psk3dx:customStatus>
  <psk3dx:userprompt>Confirm the 3D printer is calibrated and ready for the next print</psk3dx:userprompt>

   <!— Additional Slicer settings follow (optional) -->

</PrintDeviceCapabilities>
```

对于不具有载入显示和按钮，以允许用户与打印开头的设备进行交互的 3D 打印机，我们大使返回使用合适的用户提示消息集的 PDC xml 中所示**psdk3dx:userPrompt**. 这是为了防止从一个现有基于新打印。 自定义状态消息*&lt;psk3dx:customStatus&gt;* 用于切片期间显示的任何消息。

### <a name="hresult-cleanuplpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT Cleanup(LPCWSTR pPrinterName, LPCWSTR pPortName, DWORD dwJobId, LPVOID\* ppPartnerData)

- **dwJobId** -用于跟踪后台处理程序中的作业的作业 id
- **pPortName** -3D 打印机的端口名
- **pPrinterName** -此打印作业发送到打印机的名称
- **ppPartnerData**的指针到指针保存作业特定数据设置 InitializePrint API 调用期间

在成功完成打印作业，或在完成打印作业的取消查询的调用清理。 用于此打印，它提供对已初始化的清理资源伙伴 DLL 的机会。

### <a name="hresult-uninstallinlpcwstr-args"></a>HRESULT 卸载 (\[在\]LPCWSTR args)

此 API uninstaling 3D 打印机设备时调用，并且提供了制造商联系，以卸载它们可能已安装的软件的机制。
