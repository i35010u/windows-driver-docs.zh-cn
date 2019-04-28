---
title: 入门指南-3D 打印机的 Microsoft 标准驱动程序
description: 3D 打印机 Microsoft 标准驱动程序允许开发人员能够轻松地使他们的打印机与 Windows 10 兼容。
ms.assetid: DAFC5B26-09BA-483C-B964-1DA96E77765F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0faefc875791e74ed3e8c8b6498a046a58640d2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328913"
---
# <a name="getting-started-guide---microsoft-standard-driver-for-3d-printers"></a>入门指南-3D 打印机的 Microsoft 标准驱动程序


3D 打印机 Microsoft 标准驱动程序允许开发人员能够轻松地使他们的打印机与 Windows 10 兼容。 使用 Microsoft 操作系统描述符的任何打印机可以识别为兼容的 3D 打印机。 使用一个具体示例，本文将演示如何创建允许在设备被识别为 3D 打印机的 Windows 10 和传达其打印功能的固件。

## <a name="introduction"></a>简介


Microsoft 标准驱动程序使从独立硬件供应商 (Ihv) 想要与 Windows 10 兼容其 3D 打印机编写其自己的驱动程序的负担。 了解 Microsoft 操作系统描述符的 Windows 版本使用控制请求检索的信息并使用它来安装和配置设备，而无需任何用户交互。

若要获取 Windows 10 上使用 3D 打印机的一般过程包括以下步骤：

1.  **兼容 ID**。 独立硬件供应商 (IHV) 都必须包括打印机在固件中的"3D 打印"兼容 ID。 这样，若要识别为 3D 打印机设备。

2.  **标准驱动程序**。 一旦在插入设备，Windows 更新将下载 3D 打印标准驱动程序并为使用默认配置 3D 打印机检测当前设备。

3.  **扩展属性描述符**。 3D 打印机的几种基本配置可作为标准驱动程序的一部分。 因此，开发人员可以选择匹配其 3D 打印机的基本配置。 顶部选择基本配置，开发人员可以重写某些更好地匹配的属性及其 3D 打印机，并将其包含在新的固件。

4.  **插**。 一旦固件刻录时 3D 打印机的闪存，每当用户将其插入到 Windows 10 计算机时，标准驱动程序将自动下载，并且将开发人员已选择的自定义打印功能。

在以下部分中，我们将说明每个步骤使用具体的示例。

有关详细信息，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?LinkId=533944)。

## <a name="compatible-id"></a>兼容 ID


若要指定 Windows 操作系统，我们当前使用的 3D 打印机，我们不得不使用右兼容 id。 Microsoft 兼容 ID 列表目前[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?LinkId=533944)。

3D 打印机的兼容 ID 表所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>兼容 ID</th>
<th>次级兼容 ID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"3DPRINT"</p>
<p>(0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00)</p></td>
<td><p>变化不定</p></td>
<td><p>MS3DPRINT G 代码打印机</p></td>
</tr>
</tbody>
</table>

 

在标头文件中包括在 3D 打印机固件，IHV 必须指定兼容 ID 如下所示：

```cpp
#define MS3DPRINT_CONFIG_SIZE 232

#define MS3DPRINT_OSP_SIZE (4+4+2+0x20+4+MS3DPRINT_CONFIG_SIZE)

#define MS3DPRINT_XPROP_SIZE (4+2+2+2+MS3DPRINT_OSP_SIZE)

#define SIZE_TO_DW(__size)                \
        ((uint32_t)__size) & 0xFF,        \
        (((uint32_t)__size)>>8) & 0xFF,   \
        (((uint32_t)__size)>>16) & 0xFF,  \
        (((uint32_t)__size)>>24) & 0xFF 

// CompatibleID and SubCompatibleID
static const uint8_t PROGMEM ms3dprint_descriptor[40] = {
    0x28, 0x00, 0x00, 0x00,                          // dwLength
    0x00, 0x01,                                      // bcdVersion
    0x04, 0x00,                                      // wIndex
    0x01,                                            // bCount
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,        // RESERVED
    0x00,                                            // bFirstInterfaceNumber
    0x01,                                            // RESERVED
    '3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")
                                                 // subCompatibleID
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00   /*        */  
,
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00               // RESERVED
};
```

上面的代码中的此行是 3D 打印机兼容 ID:

`'3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")`

使用此特定的配置，Ihv 可以编译其固件和闪存设备。 然后在插入设备，从 Windows 更新将自动获取下载 3D 打印标准驱动程序。

在此阶段的打印机使用标准驱动程序默认配置，使用默认配置的参数是可在文件夹 %SYSTEMROOT%中访问\\System32\\MS3DPrint StandardGCode.xml 文件中的。 此外，开发人员可以选择要使用不同的基本配置，基本配置的列表位于同一文件夹 %SYSTEMROOT%\\System32\\MS3DPrint。 此列表中随着新 3D 打印机出现在市场上定期填充了新的配置。

## <a name="extended-properties-os-feature-descriptor"></a>扩展属性操作系统功能描述符


如上述部分中所述，Ihv 将有权访问多个基本配置。 最大程度减少必须存储在打印机的闪存的信息量优点。 开发人员可以检查提供的基本配置，并选择最接近于他们的打印机。 在此示例中我们要选择的 SD 卡基本配置和重写属性，使用以下参数：

| Parameters            | ReplTest1  |
|-----------------------|--------|
| Job3DOutputAreaWidth  | 250000 |
| Job3DOutputAreaDepth  | 260000 |
| Job3DOutputAreaHeight | 270000 |
| Filamentdiameter      | 2850   |

 

有关这些参数的详细信息，请参阅*MS3DPrint 标准 G 代码 Driver.docx*中的文档[3D 打印 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)文档。

若要指定要使用的基本配置和重写的参数，开发人员可以通过扩展属性操作系统功能描述符指定它，如下所示：

```cpp
// Modifiers to the base configuration
static const uint8_t PROGMEM ms3dprint_properties_descriptor[] = {
    SIZE_TO_DW(MS3DPRINT_XPROP_SIZE),                   // dwLength
    0x00, 0x01,                                         // bcdVersion
    0x05, 0x00,                                         // wIndex
    0x01, 0x00,                                         // wCount
    
    SIZE_TO_DW(MS3DPRINT_OSP_SIZE),                     // dwSize
    0x07, 0x00, 0x00, 0x00,                             // dwPropertyDataType  (1=REG_SZ, 4=REG_DWORD, 7=REG_MULTI_SZ)

    0x20, 0x00,                                         // wPropertyNameLength
    'M', 0x0, 'S', 0x0, '3', 0x0, 'D', 0x0,             // bPropertyName
    'P', 0x0, 'r', 0x0, 'i', 0x0, 'n', 0x0,
    't', 0x0, 'C', 0x0, 'o', 0x0, 'n', 0x0,
    'f', 0x0, 'i', 0x0, 'g', 0x0, 0x0, 0x0,

    SIZE_TO_DW(MS3DPRINT_CONFIG_SIZE),                  // dwPropertyDataLength

    // Data
    0x42, 0x00, 0x61, 0x00, 0x73, 0x00, 0x65, 0x00, 0x3D, 0x00, 0x53, 0x00, 0x44, 0x00, 0x00, 0x00,  /* Base=SD  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x57, 0x00,  /* putAreaW */  
    0x69, 0x00, 0x64, 0x00, 0x74, 0x00, 0x68, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x35, 0x00, 0x30, 0x00,  /* idth=250 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00,  /* 000 Job3 */  
    0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00, 0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00,  /* DOutputA */  
    0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x44, 0x00, 0x65, 0x00, 0x70, 0x00, 0x74, 0x00, 0x68, 0x00,  /* reaDepth */  
    0x3D, 0x00, 0x32, 0x00, 0x36, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00,  /* =260000  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x48, 0x00,  /* putAreaH */  
    0x65, 0x00, 0x69, 0x00, 0x67, 0x00, 0x68, 0x00, 0x74, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x37, 0x00,  /* eight=27 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x66, 0x00, 0x69, 0x00, 0x6C, 0x00,  /* 0000 fil */  
    0x61, 0x00, 0x6D, 0x00, 0x65, 0x00, 0x6E, 0x00, 0x74, 0x00, 0x64, 0x00, 0x69, 0x00, 0x61, 0x00,  /* amentdia */  
    0x6D, 0x00, 0x65, 0x00, 0x74, 0x00, 0x65, 0x00, 0x72, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x38, 0x00,  /* meter=28 */  
    0x35, 0x00, 0x30, 0x00, 0x00, 0x00, 0x00, 0x00                                                   /* 50       */  
};
```

有关扩展的属性操作系统功能描述符信息位于*OS\_Desc\_Ext\_Prop.doc*文件。 请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?LinkId=533944)有关详细信息。

## <a name="verifying-the-print-capabilities"></a>验证打印功能


一旦该设备已刻录到闪存中的固件，设备将自动检测到 Windows 10 和打印功能将存储在注册表中。

![安装兼容 3d 打印机 ](images/installing-compatible-3d-printer.png)

它是非常重要，IHV 对自己更改设备 VID/PID。 永远不应使用供应商 ID (VID) 或产品 ID (PID) 的另一台现有设备，因为操作系统将无法正确检测到设备，如 VID 和 PID 将优先于操作系统描述符。

如果已正确安装该设备，设备应列入**设备和打印机**。

![“设备和打印机”](images/devices-and-printers-3d.png)

在中**设备管理器**，可以验证设备 id 和兼容 id 匹配。

![“设备管理器”](images/device-manager-3d.png)

![设备管理器详细信息选项卡-匹配设备 id](images/device-manager-details-3d.png)

![设备管理器详细信息选项卡-兼容 id](images/device-manager-details2-3d.png)

可以通过访问注册表中的获得 USB 驱动程序属性**HKEY\_本地\_机\\系统\\CurrentControlSet\\枚举\\USB**.

![编辑 usb 注册表中的多字符串值](images/usb-registry-3d.png)

可以通过访问注册表中的获得 3D 打印驱动程序属性**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\打印\\打印机**。

![在注册表中查看 3d 打印驱动程序属性](images/printers-registry-3d.png)

## <a name="additional-resources"></a>其他资源


有关详细信息，请参阅以下文档和资源：

[在 Windows 中的 3D 打印](https://go.microsoft.com/fwlink/p/?LinkId=534206)

[3D 打印 SDK （MSI 下载）](https://go.microsoft.com/fwlink/p/?LinkId=394375)

[Microsoft OS Descriptors](https://go.microsoft.com/fwlink/p/?LinkId=533944)

[USB 2.0 规范](https://go.microsoft.com/fwlink/p/?linkid=533945)

您也可以联系 Microsoft 3D 打印团队在[提出 3D 打印问题](https://go.microsoft.com/fwlink/p/?LinkId=534751)(ask3dprint@microsoft.com)。

 

 




