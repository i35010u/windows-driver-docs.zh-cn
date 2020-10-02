---
title: 3D 打印机的自定义 USB 接口支持
description: 本主题介绍如何为 v3 和 v4 打印驱动程序生态系统中的3D 打印机启用自定义 USB 接口。
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: b660523c75d72a8b450633dd8849f46c62193d3e
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662345"
---
# <a name="enable-a-custom-usb-interface-for-a-3d-printer"></a>为3D 打印机启用自定义 USB 接口

本主题中所述的体系结构支持在 v3 和 v4 print 生态系统中支持自定义 USB 接口3D 打印机。 标准端口监视器 **3dmon.dll**向使用本地服务凭据运行的 Windows **3DPrintService** 转发3d 打印作业命令。 服务将加载并与伙伴 DLL 通信，以执行三维打印作业所需的自定义命令。 伙伴 DLL 以及 **3dmon.dll** 和 **3dprintservice.exe** 可再发行组件都由设备的 USB 驱动程序包安装。 伙伴 DLL 必须实现和导出一组函数以便与 **3DPrintService**进行通信。 与打印后台处理程序服务交互所需的其他功能在 **3dmon.dll**中实现。

> [!NOTE]
> 此体系结构要求伙伴 DLL 为多实例线程安全。

## <a name="architecture-decisions"></a>体系结构决策

**3DPrintService** windows 服务用于在打印工作流期间在合作伙伴提供的 dll 中加载和调用特定定义的 api。 这些 Api 允许与打印机通信。

KMDF USB 筛选器驱动程序包发布在 Windows 更新上，以便通过 PnP 为受支持的3D 打印机安装。 KMDF 驱动程序安装合作伙伴软件并创建3D 打印机设备节点。 3D 打印机设备节点是使用 Windows 更新中的合作伙伴发布的 v4 打印驱动程序安装的。

## <a name="packaging-decisions"></a>打包决策

### <a name="binaries-and-binary-dependencies"></a>二进制文件和二进制依赖项

Architectue 使用硬件制造商在 Windows 更新上发布的驱动程序。 此驱动程序包括以下 Microsoft 提供的可再发行二进制文件及其依赖项：

- 3dmon.dll
- 3dprintservice.exe
- ms3dprintusb.sys

#### <a name="kernel-mode-usb-filter-driver"></a>内核模式 USB 筛选器驱动程序

KMDF 驱动程序由合作伙伴发布，由下图所示的组件组成。 这会将设备与硬件 ID （ (通常为 VID & PID) ）相匹配。 驱动程序在安装时创建一个3D 打印机设备节点，该节点将触发打印队列和切片器驱动程序的安装。 创建的3D 打印机设备节点的合作伙伴 provids v4 打印机驱动程序。

![kmdf usb 筛选器驱动程序](images/kmdf-usb-filter-driver.png)

##### <a name="ms3dprintusbsys"></a>MS3DPrintUSB.sys

在 Enum 3DPrint 下创建3D 打印机开发节点的内核模式设备驱动程序 \\ 。 PnP 子系统通过基于 Winusb.sys 创建的设备节点直接匹配 VID & PID 来调用它。 如果系统) 上尚未安装，则驱动程序 .inf 文件将设置用于设置 **3DPrintService** (的自定义 DLL。

##### <a name="3dmondll"></a>3dmon.dll

3DMon.dll 是由 Microsoft 发布的端口监视器可再发行的二进制文件，由后台处理程序调用以与3D 打印机通信。

##### <a name="3dprintserviceexe"></a>3dprintservice.exe

3DPrintService.exe 是在驱动程序安装过程中作为 Windows 服务安装的 Microsoft 发布的二进制文件。 3DMon 与此服务通信，以执行打印、双向等操作和3D 打印机。

##### <a name="partnerimpldll"></a>Partnerimpl.dll

Partnerimp.dll 是合作伙伴的已发布 Microsoft 界面实现。 DLL 使用其协议与伙伴的设备通信。 3DPrintService.exe 在运行时加载此 DLL 来驱动3D 打印机设备的操作。

![显示3个打印机设备操作的设备通信流的关系图。](images/3dprintservice.png)

### <a name="printer-usage-sequence"></a>打印机使用顺序

- 后台处理程序与将命令发送到 3DPrintService windows 服务的 3dmon.dll 进行通信
- 3DPrintService.exe 以 NetworkService 的帐户凭据运行
- 当使用三维打印机时，后台处理程序通过 3dmon.dll 会将命令发送到3DPrintService
- 3DPrintService 在合作伙伴提供的实现 Dll 上处理命令并调用 Api
- 3DPrintService 将来自合作伙伴提供的 Dll 的响应移交回后台处理程序

## <a name="interfaces-and-interactions"></a>接口和交互

合作伙伴 DLL 必须导出以下 API 函数：

### <a name="hresult-installin-lpcwstr-args"></a>HRESULT \[ 在 LPCWSTR 参数中安装 (\]) 

此 API 是可选的，可供制造商用来为其设备安装自定义软件或注册。 例如，安装包含在设备的驱动程序包中的建模。 使用系统凭据调用此 API 以启用安装。

### <a name="dword-printapisupported"></a>DWORD PrintApiSupported ( # A1

第三方制造商使用此 API 来指示支持的3D 打印服务 API 版本。 以下 Api 与3DPrintService 的版本1兼容。

### <a name="hresult-initializeprintlpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT InitializePrint (LPCWSTR pPrinterName、LPCWSTR pPortName、DWORD dwJobId、LPVOID \* ppPartnerData) 

此 API 是在打印事件开始初始化打印机之前调用的。 打印机可以在 ppPartnerData 参数中保存特定于作业的状态。 此调用类似于 StartDocPort 调用。

- **jobId** -用于跟踪作业的作业 id
- **portvalue** -3d 打印机的 portvalue
- **printerName** -要将打印作业发送到的打印机的名称
- **ppPartnerData** -指向可用于存储任何特定于作业的数据的指针

### <a name="hresult-printfilein-dword-jobid-in-lpwstr-portname-in-lpwstr-printername-in-lpwstr-pathtorenderedfileinlpvoid-pppartnerdata"></a>HRESULT PrintFile (\[ in \] DWORD jobId， \[ \] LPWSTR portvalue， \[ \] LPWSTR printerName \[ \] \[ \] \* ，LPWSTR pathToRenderedFile，LPVOID ppPartnerData) 

第三方制造商使用此 API 在其打印机上打印文档。

- **jobId** -用于跟踪作业的作业 id
- **portvalue** -3d 打印机的 portvalue
- **printerName** -要将打印作业发送到的打印机的名称
- **pathToRenderedFile** -执行渲染后假脱机文件所在位置的 UNC 路径。 第三方制造商处理此位置中的文件，并在其设备上打印文档
- **ppPartnerData** -指向 isused 的指针，用于在 InitializePrint API 调用期间存储特定于伙伴的数据设置。
- 可使用端口名称从注册表中获取**printerName** 。 第三方制造商 maynot 可以使用端口名称与其设备通信。 打印机名称在 Windows 计算机上是唯一的，其软件将能够确定要打印作业的打印机。 在计算机上处于活动状态的所有打印机都可以在以下注册表项中找到：

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 打印 \\ 打印机**

![3d 打印机注册表](images/3d-printer-registry.png)

### <a name="hresult-query_in_-lpcwstr-command-_in_-lpcwstr-commanddata-_out_-lpwstr-resultbuffer-_out_-resultbuffersize--_in_-lpvoid-pppartnerdata"></a>HRESULT 查询 (\_ 在 \_ LPCWSTR 命令中， \_ 在 \_ LPCWSTR CommandData， \_ out \_ LPWSTR resultBuffer， \_ out \_ resultBufferSize，， \_ \_ LPVOID \* ppPartnerData) 

- 作为查询发送的**命令**字符串命令
- **commandData** 参数 (可选) 
- **resultBuffer** -查询参数调用的结果>
- **resultBufferSize** -结果缓冲区字符串的大小
- **ppPartnerData** -指向当前合作伙伴 DLL 实例的指针的指针

3Dprint 服务调用伙伴 DLL 以获取要为命令分配的缓冲区的大小。

分配用于保存响应字符串的内存后，将再次调用 DLL 以获取实际结果。

DLL 可以使用以前的 ** ( IntializePrint ** 中的实例数据与设备进行通信，而无需在每次调用 **查询 ( # B3 ** 函数时打开新的通信通道。

此 API 用于与打印机进行通信，以获取有关设备配置和打印进度的信息，或者通知伙伴 DLL 设备的拔出事件。

此制造商必须支持以下命令：

| 命令 | CommandData | 输出 | 注释 |
|---------|-------------|--------|----------|
| \\\\3DPrint： JobStatus | | 作业开始 = {"Status"： "ok"} <br> 要在完成时使用的状态： "已完成"} | 后台处理程序将在打印队列 UI 中显示返回的任何值。 这允许设备在打印队列 UI 上打印时显示相关信息。 设备可在此处返回任意字符串 (例如 "忙" 或 "33% complete" ) ，这会在打印队列作业状态中逐字显示。 |
| \\\\3DPrint： JobCancel | | {"Status"： "已完成"} | 当用户取消打印时，后台处理程序将调用此命令。 当取消成功并且句柄和线程已关闭时，伙伴 DLL 返回此值。 |
| \\\\打印机功能：数据 | | 符合 PrintDeviceCapabilites (PDC) 架构的 XML 字符串。 | PDC 查询由想要获取有关打印机的详细信息的应用程序调用。 数据用于描述设备的功能，如果驱动程序依赖于 Microsoft 切片器，则可以包括切片器设置。 请参阅下面的示例 PDC。 |
| \\\\3DPrint：断开连接 | | {"Status"： "OK"} | 此查询在打印机设备的 PnP 断开连接时触发。 合作伙伴可以执行任何所需的操作，例如关闭任何打开的句柄以允许正确重新连接。 |
| \\\\3DPrint： Connect | | {"Status"： "OK"} | 当打印机设备存在 PnP 连接时，将触发此查询。 合作伙伴可以执行任何所需的操作。 |

#### <a name="print-device-capabilities-xml"></a>打印设备功能 XML

以下打印设备功能 XML 可用作示例：

```xml
<?xml version="1.0"?>
<PrintDeviceCapabilities
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema"
    xmlns:xml="https://www.w3.org/XML/1998/namespace"
    xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:psk3dx="https://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywords3dextended"
    xmlns:pskv="https://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywordsvendor"
    xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:psf2="https://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    xmlns="https://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
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

对于没有机载显示和按钮的3D 打印机，若要使用户能够在打印开始时与设备交互，我们鼓励返回一个 PDC xml，其中包含 **psdk3dx： userPrompt**中的相应用户提示消息集。 这是为了防止在现有打印时开始新打印。 自定义状态消息* &lt; Psk3dx： customStatus &gt; *用于在切片期间显示任何消息。

### <a name="hresult-cleanuplpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT 清除 (LPCWSTR pPrinterName、LPCWSTR pPortName、DWORD dwJobId、LPVOID \* ppPartnerData) 

- **dwJobId** -用于在后台处理程序中跟踪作业的作业 id
- **pPortName** -3d 打印机的 portvalue
- **pPrinterName** -要将打印作业发送到的打印机的名称
- **ppPartnerData** -指针，用于在 InitializePrint API 调用期间保存特定于作业的数据设置

当打印作业成功完成时，或在完成对打印作业的 cancel 查询时调用清除。 它为合作伙伴 DLL 提供了清理为此打印初始化的资源的机会。

### <a name="hresult-uninstallinlpcwstr-args"></a>HRESULT 卸载 (\[ \] LPCWSTR 参数) 

当 uninstaling 3D 打印机设备并为制造商提供卸载可能已安装的软件的机制时，将调用此 API。
