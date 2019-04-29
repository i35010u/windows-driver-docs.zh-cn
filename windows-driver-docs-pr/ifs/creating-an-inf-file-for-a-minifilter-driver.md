---
title: 创建用于微筛选器驱动程序的 INF 文件
description: 创建用于微筛选器驱动程序的 INF 文件
ms.assetid: 2ae41287-e3c5-4df5-8dec-8575343d5319
keywords:
- INF 文件 WDK 文件系统微筛选器驱动程序
- DestinationDirs 部分 WDK 文件系统
- 版本部分 WDK 文件系统
- 字符串部分 WDK 文件系统
- DefaultUninstall 部分 WDK 文件系统
- ServiceInstall 部分 WDK 文件系统
- DefaultInstall 部分 WDK 文件系统
- AddRegistry 部分 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90713fedfef6f76bb2c6eeaa2910bf9447fb9756
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370721"
---
# <a name="creating-an-inf-file-for-a-minifilter-driver"></a>创建用于微筛选器驱动程序的 INF 文件


## <span id="ddk_creating_an_inf_file_for_a_minifilter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_MINIFILTER_DRIVER_IF"></span>


文件系统微筛选器驱动程序的 INF 文件通常包含以下部分：

版本 （必需）

DestinationDirs （可选但建议使用）

DefaultInstall （必需）

DefaultInstall.Services （必需）

ServiceInstall （必需）

AddRegistry （必需）

DefaultUninstall （可选）

DefaultUninstall.Services （可选）

字符串 （必需）

**请注意**  从基于 x64 的 Windows Vista 系统，所有内核模式组件，包括非 PnP （插） 驱动程序，例如文件系统驱动程序 （文件系统、 旧筛选器，以及微筛选器驱动程序），必须进行签名的顺序若要加载和执行。 对于此方案中，以下列表包含与文件系统驱动程序相关的信息：
-   对于非 PnP 驱动程序，包括文件系统驱动程序的 INF 文件不需要包含\[制造商\]或\[模型\]部分。

-   [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令行工具，位于\\bin\\SelfSign WDK 安装目录，目录可用于直接"嵌入符号"驱动程序 SYS可执行文件。 出于性能原因，引导启动驱动程序必须包含嵌入式的签名。

-   给定的 INF 文件，请[Inf2cat](https://go.microsoft.com/fwlink/p/?linkid=79443)命令行工具可用于创建驱动程序包的目录 (.cat) 文件。 仅目录文件可以接收[WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)徽标签名。

-   使用管理员权限，仍可与 Windows Vista 一起启动的基于 x64 的系统上安装未签名的驱动程序。 但是，该驱动程序将无法加载 （并因此执行） 因为它是无符号。

-   有关签名的驱动程序的常规信息，请参阅[驱动程序签名](https://msdn.microsoft.com/library/windows/hardware/ff544865)。

-   驾驶签名过程的详细信息，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

-   所有内核模式组件，包括自定义内核模式开发工具，必须进行都签名。 有关详细信息，请参阅[签名驱动程序开发和测试 （Windows Vista 和更高版本） 期间](https://msdn.microsoft.com/library/windows/hardware/ff552275)。

 

### <a name="span-idversionsectionrequiredspanspan-idversionsectionrequiredspanspan-idversionsectionrequiredspanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>版本部分 （必需）

[**版本**](https://msdn.microsoft.com/library/windows/hardware/ff547502)部分指定的类和取决于微筛选器驱动程序的类型的 GUID，如下面的代码示例中所示。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 10/09/2001,1.0.0.0
CatalogFile = 
```

下表显示的值应该在中指定文件系统微筛选器驱动程序[**版本**](https://msdn.microsoft.com/library/windows/hardware/ff547502)部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>签名</strong></p></td>
<td align="left"><p>"$WINDOWS NT $"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>类</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 Guid</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 Guid</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>提供程序</strong></p></td>
<td align="left"><p>在您自己的 INF 文件，应指定 Microsoft 以外的提供程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547394)"> <strong>INF DriverVer 指令</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>对于已签名的防病毒微筛选器驱动程序，此条目包含 WHQL 提供目录文件的名称。 所有其他微筛选器驱动程序应将此项留空。 有关详细信息，请参阅的说明<strong>CatalogFile</strong>中的条目<a href="https://msdn.microsoft.com/library/windows/hardware/ff547502" data-raw-source="[&lt;strong&gt;INF Version Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547502)"> <strong>INF 版本部分</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>（可选但建议这样做） DestinationDirs 部分

[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)部分指定将在其中复制微筛选器驱动程序和应用程序文件的目录。

在本部分中并在**ServiceInstall**部分中，您可以指定的已知的系统目录，系统定义的数字值。 有关这些值的列表，请参阅[ **INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)。 在下面的代码示例中，值 12 引用的驱动程序目录 (%windir%\\system32\\驱动程序)，而值 10 指 Windows 目录 （%windir%)。

```cpp
[DestinationDirs]
DefaultDestDir = 12
Minispy.DriverFiles = 12
Minispy.UserFiles   = 10,FltMgr
```

### <a name="span-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>DefaultInstall 部分 （必需）

在中[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356)部分中， [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)指令将微筛选器驱动程序的驱动程序文件和用户应用程序复制文件中指定的目标[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)部分。

**请注意**   [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)目录文件或 INF 文件本身不应引用指令。 安装程序 Api 将自动复制这些文件。

 

可以创建一个 INF 文件在多个版本的 Windows 操作系统上安装的驱动程序。 您可以通过创建其他创建此类型的 INF 文件[ **DefaultInstall**](https://msdn.microsoft.com/library/windows/hardware/ff547356)， [ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)， **DefaultUninstall**，并**DefaultUninstall.Services**的部分，了解每个操作系统版本。 每个部分都标有*修饰*（如.ntx86、.ntia64 或.nt），指定它所应用于的操作系统版本。 有关创建此类型的 INF 文件的详细信息，请参阅[创建多个平台和操作系统的 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff540206)。

下面的代码示例显示了典型[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356)部分。

```cpp
[DefaultInstall]
OptionDesc = %MinispyServiceDesc%
CopyFiles = Minispy.DriverFiles, Minispy.UserFiles
```

### <a name="span-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>DefaultInstall.Services 部分 （必需）

[ **DefaultInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547360)部分包含[ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)指令，用于控制如何以及何时的服务加载特定的驱动程序，如下面的代码示例中所示。

```cpp
[DefaultInstall.Services]
AddService = %MinispyServiceName%,,Minispy.Service
```

### <a name="span-idserviceinstallsectionrequiredspanspan-idserviceinstallsectionrequiredspanspan-idserviceinstallsectionrequiredspanserviceinstall-section-required"></a><span id="ServiceInstall_Section__required_"></span><span id="serviceinstall_section__required_"></span><span id="SERVICEINSTALL_SECTION__REQUIRED_"></span>ServiceInstall 部分 （必需）

**ServiceInstall**部分包含用于加载的驱动程序服务的信息。 MiniSpy 示例驱动程序，在本部分是名为"Minispy.Service"，如下面的代码示例中所示。 名称**ServiceInstall**部分必须出现在[ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)指令[ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)部分。

```cpp
[Minispy.Service]
DisplayName    = %MinispyServiceName%
Description    = %MinispyServiceDesc%
ServiceBinary  = %12%\minispy.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = Minispy.AddRegistry
Dependencies   = FltMgr
```

**ServiceType**条目指定的服务的类型。 微筛选器驱动程序应指定值 2 (服务\_文件\_系统\_驱动程序)。 有关详细信息**ServiceType**条目，请参阅[ **INF AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326)。

**StartType**条目指定在启动服务。 下表列出了可能的值为**StartType**和及其相应的启动类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_BOOT_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_SYSTEM_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_AUTO_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_DEMAND_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>SERVICE_DISABLED</p></td>
</tr>
</tbody>
</table>

 

详细了解这些启动类型，请参阅中"驱动程序启动类型"[确定当驱动程序加载的内容](what-determines-when-a-driver-is-loaded.md)。

**LoadOrderGroup**条目提供的信息，因此需要确保微筛选器驱动程序和旧的文件系统筛选器驱动程序之间的互操作性的筛选器管理器。 应指定**LoadOrderGroup**适合于正在开发的微筛选器驱动程序的类型的值。 若要选择加载顺序组，请参阅[加载顺序组和海拔微筛选器驱动程序的地区](load-order-groups-and-altitudes-for-minifilter-drivers.md)。

请注意，必须指定**LoadOrderGroup**值，即使微筛选器驱动程序的启动类型不是服务\_启动\_开始。 在这种方式，微筛选器驱动程序是不同于传统的文件系统筛选器驱动程序。

**请注意**  筛选器管理器**StartType**值是服务\_启动\_开始，并将其**LoadOrderGroup**值是 FSFilter 基础结构. 这些值可确保任何微筛选器驱动程序加载之前始终处于加载筛选器管理器。

 

详细了解如何**StartType**并**LoadOrderGroup**条目确定加载驱动程序时，请参阅[确定当驱动程序加载的内容](what-determines-when-a-driver-is-loaded.md)。

**请注意**  微筛选器驱动程序，请与旧的文件系统筛选器驱动程序，不同**StartType**并**LoadOrderGroup**值不用于确定在何处微筛选器驱动程序将附加微筛选器实例堆栈中。 此位置是取决于微筛选器实例指定海拔高度。

 

**ErrorControl**条目指定服务在系统启动期间启动失败时要采取的操作。 微筛选器驱动程序应指定的值为 1 (服务\_错误\_正常)。 有关详细信息**ErrorControl**条目，请参阅[ **INF AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326)。

[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)指令是指编写器定义的一个或多个 INF **AddRegistry**部分，其中包含要存储在注册表中的新安装信息服务。 微筛选器驱动程序使用**AddRegistry**部分定义微筛选器驱动程序实例并指定默认实例。

**依赖项**条目指定的任何服务或驱动程序所依赖的加载顺序组的名称。 所有微筛选器驱动程序必须指定 FltMgr，即筛选器管理器的服务名称。

### <a name="span-idaddregistrysectionrequiredspanspan-idaddregistrysectionrequiredspanspan-idaddregistrysectionrequiredspanaddregistry-section-required"></a><span id="AddRegistry_Section__required_"></span><span id="addregistry_section__required_"></span><span id="ADDREGISTRY_SECTION__REQUIRED_"></span>AddRegistry 部分 （必需）

**AddRegistry**部分向注册表添加项和值。 微筛选器驱动程序使用**AddRegistry**部分定义微筛选器实例并指定默认实例。 每当筛选器管理器创建微筛选器驱动程序的新实例时，将使用此信息。

在 MiniSpy 示例驱动程序，以下**AddRegistry**部分中，与中的 %strkey%令牌定义一起[**字符串**](https://msdn.microsoft.com/library/windows/hardware/ff547485)部分中，定义三个实例，其中一个命名为 MiniSpy 示例驱动程序的默认实例。

```cpp
[Minispy.AddRegistry]
HKR,%RegInstancesSubkeyName%,%RegDefaultInstanceValueName%,0x00000000,%DefaultInstance%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegAltitudeValueName%,0x00000000,%Instance1.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegFlagsValueName%,0x00010001,%Instance1.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegAltitudeValueName%,0x00000000,%Instance2.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegFlagsValueName%,0x00010001,%Instance2.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegAltitudeValueName%,0x00000000,%Instance3.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegFlagsValueName%,0x00010001,%Instance3.Flags%
```

### <a name="span-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall 部分 （可选）

**DefaultUninstall**部分是可选的但建议执行，如果可以卸载您的驱动程序。 它包含[ **DelFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547363)并[ **DelReg** ](https://msdn.microsoft.com/library/windows/hardware/ff547374)指令以删除文件和注册表项，如下面的代码示例中所示。

```cpp
[DefaultUninstall]
DelFiles   = Minispy.DriverFiles, Minispy.UserFiles
DelReg     = Minispy.DelRegistry
```

### <a name="span-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall.Services 部分 （可选）

**DefaultUninstall.Services**部分是可选的但建议执行，如果可以卸载您的驱动程序。 它包含[ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)指令以删除微筛选器驱动程序的服务，如下面的代码示例摘自 MiniSpy 示例驱动程序中所示。

**请注意**   [ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)指令应始终指定 SPSVCINST\_STOPSERVICE 标志 (0x00000200) 删除之前停止服务。

 

```cpp
[DefaultUninstall.Services]
DelService = Minispy,0x200
```

### <a name="span-idstringssectionrequiredspanspan-idstringssectionrequiredspanspan-idstringssectionrequiredspanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>（必需） 的字符串部分

[**字符串**](https://msdn.microsoft.com/library/windows/hardware/ff547485)部分定义 INF 文件中使用的每个 %strkey%标记。

可以通过创建其他特定于区域设置创建一个国际 INF 文件**字符串。**<em>LanguageID</em> INF 文件中的部分。 有关国际 INF 文件的详细信息，请参阅[创建国际 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff540208)。

下面的代码示例显示了典型[**字符串**](https://msdn.microsoft.com/library/windows/hardware/ff547485)部分。

```cpp
[Strings]
Msft               = "Microsoft Corporation"
MinispyServiceDesc = "Minispy mini-filter driver"
MinispyServiceName = "Minispy"
RegInstancesSubkeyName = "Instances"
RegDefaultInstanceValueName  = "DefaultInstance"
RegAltitudeValueName    = "Altitude"
RegFlagsValueName  = "Flags"

DefaultInstance    = "Minispy - Top Instance"
Instance1.Name     = "Minispy - Middle Instance"
Instance1.Altitude = "370000"
Instance1.Flags    = 0x1 ; Suppress automatic attachments
Instance2.Name     = "Minispy - Bottom Instance"
Instance2.Altitude = "365000"
Instance2.Flags    = 0x1 ; Suppress automatic attachments
Instance3.Name     = "Minispy - Top Instance"
Instance3.Altitude = "385000"
Instance3.Flags    = 0x1 ; Suppress automatic attachments
```

 

 




