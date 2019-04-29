---
title: XPS 驱动程序文档事件
description: XPS 驱动程序文档事件
ms.assetid: 240e14d1-d8ee-403c-b728-b14941775634
keywords:
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，事件
- 事件 WDK XPSDrv
- 通知 WDK XPSDrv
- DrvDocumentEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8d1d67663b6d33f8d8d144636ac3b7531a47399
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390914"
---
# <a name="xps-driver-document-events"></a>XPS 驱动程序文档事件


Microsoft Windows Presentation Foundation (WPF) 打印支持 XPSDrv 打印驱动程序通知将事件发送在类似于 GDI 打印支持如何将通知发送给 GDI 打印驱动程序文档后台处理过程。 WPF 打印支持也使用相同**DrvDocumentEvent** GDI 打印支持使用 DDI 函数，但新的事件具有已定义为支持 XPS 文档处理事件。 GDI 打印支持会继续发出**DrvDocumentEvent**基于 GDI 的打印驱动程序和 XPSDrv 的事件处理程序打印的 Microsoft Win32 应用程序打印驱动程序。

### <a name="drvdocumentevent-event-handler-overview"></a>DrvDocumentEvent 事件处理程序概述

如果有必要，XPSDrv 打印驱动程序可以将导出**DrvDocumentEvent**配置模块中为截距文档处理函数的事件处理程序。 与新的 XPS 文档相关的事件由符号名称以与"DOCUMENTEVENT\_XPS\_"。

WPF 打印支持调用**DrvDocumentEvent** XPSDrv 打印驱动程序的后台处理打印文档时的函数。 每次调用发生在流程中的不同步骤。 值由标识每个调用的处理步骤*iEsc*参数。 所引用的缓冲区的内容*pvIn*并*pvOut*参数不同，具体取决于处理步骤。

本主题中的以下各个小节介绍了 WPF 打印支持生成的 XPS 文档处理事件。

### <a name="drvdocumentevent-event-handler-description"></a>DrvDocumentEvent 事件处理程序描述

**DrvDocumentEvent**事件处理程序具有以下调用格式。 在本部分中的代码和参数定义仅适用于信息。

```cpp
INT
  DrvDocumentEvent(
    HANDLE  hPrinter,
    HDC  hdc,
    int  iEsc,
    ULONG  cbIn,
    PVOID  pvIn,
    ULONG  cbOut,
    PVOID  pvOut
    );
```

### <a name="parameters"></a>Parameters

<a href="" id="hprinter"></a>*hPrinter*  
打印机句柄的 WPF 打印支持提供。

<a href="" id="hdc"></a>*hdc*  
调用方提供的设备上下文句柄**CreateDC**调用生成。 (**CreateDC** Microsoft Windows SDK 文档中所述。)此参数是零个 if *iEsc*设置为 DOCUMENTEVENT\_CREATEDCPRE。

打印文档时，系统将使用相同的事件值的 XPS 和 GDI 文档。 该驱动程序必须能够识别这种相似性并确定基于作业的类型*hdc*。 *hdc*等于无效\_处理\_值为所有 DOCUMENTEVENT\_XPS\_*Xxx*事件。 此检查将确定正确的解释**DrvDocumentEvent**事件值基于调用的应用程序。 此检查也适用于 XPSDrv 打印仅限驱动程序。

<a href="" id="iesc"></a>*iEsc*  
标识要处理的事件的调用方提供转义代码。 此参数可以是以下整数常量之一。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT\_查询筛选器   
WPF 打印支持发送该事件来查询有关 XPS 文档的列表的打印驱动程序在处理该驱动程序将响应的事件。 在任何其他与 XPS 文档相关的事件之前发出此事件。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE  
WPF 打印支持会发送此事件之前它将 FixedDocumentSequence 添加到 XPS 假脱机文件。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPOST  
WPF 打印支持会发送此事件后它将 FixedDocumentSequence 添加到 XPS 假脱机文件。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRE  
WPF 打印支持会发送此事件之前它将 FixedDocument 添加到 XPS 假脱机文件。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPOST  
WPF 打印支持会发送此事件后它将 FixedDocument 添加到 XPS 假脱机文件。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
WPF 是要将 PrintTicket 添加到 FixedDocumentSequence （作业级别）。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST  
WPF 应释放该驱动程序返回到相应 datathat **DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE**事件。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
WPF 即将 PrintTicket 向 FixedDocument （文档级别）。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOST  
WPF 应释放相应 DOCUMENTEVENT 的驱动程序返回的数据\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE 事件。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
WPF 是要将 PrintTicket 添加到 FixedPage （页面级别）。

<a href="" id="documentevent-xps-addfixedpageprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOST  
WPF 释放数据的驱动程序将返回上相应 DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE 事件。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT\_XPS\_CANCELJOB  
WPF 打印支持会发送此事件之前它将调用取消作业操作。

<a href="" id="documentevent-xps-commitjob"></a>DOCUMENTEVENT\_XPS\_COMMITJOB  
WPF 完成写入当前文件的日期。

<a href="" id="cbin"></a>*cbIn*  
以字节为单位的缓冲区的大小， *pvln*参数引用。 此值是提供的 WPF 打印支持，由事件处理程序读取。

<a href="" id="pvin"></a>*pvIn*  
调用方提供的指针。 此参数的用法取决*iEsc*值，如下面的列表中所述。 (有关 DOCUMENTEVENT\_XPS\_*Xxx*未显示在此列表中，事件*pvIn*不使用。)

<a href="" id="documentevent-queryfilter"></a>DOCUMENTEVENT\_查询筛选器  
*pvIn*指向 PDOCEVENT\_筛选器结构 (与 DOCUMENTEVENT 相同\_查询筛选器)。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE  
*pvIn*点为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含三个属性：

-   EscapeCode 是 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。 EscapeCode 事件值。

-   JobIdentifier，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。 JobIdentifier 是调用 GetJob() 所需的 ID 和**SetJob**（)。

-   JobName 是 EPrintPropertyType:: kPropertyTypeString (UNICODE) 值。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPOST  
DOCUMENTEVENT 一样\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRE  
*pvIn*点到 PrintPropertiesCollection 结构 （请参阅 Winspool.h），它包含两个属性：

-   EscapeCode，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。 EscapeCode 事件值。

-   DocumentNumber，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPOST  
DOCUMENTEVENT 一样\_XPS\_ADDFIXEDDOCUMENTPRE。

<a href="" id="documentevent-xps-addfixedpagepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRE  
*pvIn*点到 PrintPropertiesCollection 结构 （请参阅 Winspool.h），它包含两个属性：

-   EscapeCode，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。

-   PageNumber，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。

<a href="" id="documentevent-xps-addfixedpagepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPOST  
DOCUMENTEVENT 一样\_XPS\_ADDFIXEDPAGEPRE。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
*pvIn*点到 PrintPropertiesCollection 结构 （请参阅 Winspool.h），它包含四个属性：

-   EscapeCode 是 EPrintPropertyType::kPropertyTypeInt32 (ULONG)。 EscapeCode 事件值。

-   JobIdentifier，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。

-   JobName 是 EPrintPropertyType:: kPropertyTypeString (UNICODE) 值。

-   PrintTicket，即 EPrintPropertyType:: kPropertyTypeByte 值。

必须将 PrintPropertiesCollection 结构和"前缀"事件的属性分配和释放它在相应的"POST"事件。 可以设置*pvOut*到**NULL**以指示支持事件，但不感兴趣更改给定的文档或页面 PrintTicket。 插件应永远不会卸载"前缀"和"POST"事件之间。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
*pvIn*是相同的指针作为从 DOCUMENTEVENT pvOut\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE

该驱动程序必须释放*pvIn*。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
*pvIn*点为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含三个属性：

-   EscapeCode，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。 EscapeCode 事件值。

-   DocumentNumber，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。

-   PrintTicket，即 EPrintPropertyType:: kPropertyTypeByte 值。

必须将 PrintPropertiesCollection 结构和"前缀"事件的属性分配和释放它在相应的"POST"事件。 可以设置*pvOut*到**NULL**以指示支持事件，但不感兴趣更改给定的文档或页面 PrintTicket。 插件应永远不会卸载"前缀"和"POST"事件之间。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOS  
*pvIn*是相同的指针作为*pvOut*从 DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE。

该驱动程序必须释放*pvIn*。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
*pvIn*点为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含三个属性：

-   EscapeCode，这是一个 EPrintPropertyType::kPropertyTypeInt32 (ULONG) 值。 EscapeCode 事件值。

-   PageNumber 是 EPrintPropertyType::kPropertyTypeInt32 (ULONG)。

-   PrintTicket，即 EPrintPropertyType:: kPropertyTypeByte。

必须将 PrintPropertiesCollection 结构和"前缀"事件的属性分配和释放它在相应的"POST"事件。 可以设置*pvOut*到**NULL**以指示支持事件，但不感兴趣更改给定的文档或页面 PrintTicket。 插件应永远不会卸载"前缀"和"POST"事件之间。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOS  
*pvIn*是相同的指针作为*pvOut*从 DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE。

该驱动程序必须释放*pvIn*。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT\_XPS\_CANCELJOB  
*pvIn*是**NULL**。

<a href="" id="cbout"></a>*cbOut*  
如果*iEsc*参数包含**DOCUMENTEVENT\_QUERYFILTER**，WPF 打印支持提供的缓冲区的大小*pvOut*参数中的引用*cbOut*参数。 对于所有其他值的*iEsc*， *cbOut*不使用。

<a href="" id="--------pvout"></a> pvOut  
提供指向 WPF 打印支持的缓冲区的指针。 缓冲区大小和内容取决于的值*iEsc*参数。 下面列出的内容*pvOut*每个缓冲区*iEsc*值。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT\_查询筛选器   
调用方提供指向的缓冲区，其中包含 DOCEVENT\_筛选器结构。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre-"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE   
一个指针为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含类型 EPrintPropertyType::kPropertyTypeBuffer"PrintTicket"属性。 此属性始终存在。 当没有 PrintTicket 可用时，PrintPropertyValue.propertyBlob.pBuf 的值是**NULL**。

属性包含 XML PrintTicket，从其 Microsoft Windows Presentation Foundation (WPF) 将而不是在使用 PrintTicket， **XPSDocumentWriter**调用方提供。 (如果*pvOut*是**NULL**属性不存在，或者属性数据是**NULL**，WPF 使用调用方提供 PrintTicket。)

处理此事件后，将调用 WPF **DocumentEvent**与 DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST 驱动程序，以释放*pvOut*。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
一个指针为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含类型 EPrintPropertyType::PropertyTypeBuffer"PrintTicket"属性。 Thisproperty 将始终存在。 可用，没有 PrintTicket 时的值**PrintPropertyValue**。 propertyBlob.pBuf 是**NULL**。

属性包含 XML PrintTicket，从中 WPF 将而不是在使用 PrintTicket， **XPSDocumentWriter**调用方提供。 (如果*pvOut*是**NULL**属性不存在，或者属性数据是**NULL**，WPF 使用调用方提供 PrintTicket。)

处理此事件后，将调用 WPF **DocumentEvent**与 DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOST 驱动程序，以释放*pvOut*。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
一个指针为 PrintPropertiesCollection 结构 （请参阅 Winspool.h） 包含"PrintTicket"类型的属性的 EPrintPropertyType::PropertyTypeBuffer。 此属性始终存在。 可用，没有 PrintTicket 时的值**PrintPropertyValue**。 propertyBlob.pBuf 是**NULL**。

属性包含 XML PrintTicket，从中 WPF 将而不是在使用 PrintTicket， **XPSDocumentWriter**调用方提供。 (如果*pvOut*是**NULL**属性不存在，或者属性数据是**NULL**，WPF 使用调用方提供 PrintTicket。)

处理此事件后，将调用 WPF **DocumentEvent**与 DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOST 驱动程序，以释放*pvOut*。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOS  
**NULL**

### <a name="return-value"></a>返回值

**DrvDocumentEvent**返回以下值之一：

<a href="" id="documentevent-success"></a>DOCUMENTEVENT\_成功  
该驱动程序已成功处理转义代码*iEsc*标识。

<a href="" id="documentevent-failure"></a>DOCUMENTEVENT\_失败  
该驱动程序支持转义代码*iEsc*标识，但出现错误。

<a href="" id="documentevent-unsupported"></a>DOCUMENTEVENT\_不受支持  
该驱动程序不支持转义代码*iEsc*标识。

### <a name="xps-document-event-structures-and-event-code-values"></a>XPS 文档事件结构和事件代码值

下面的代码示例显示的结构和新的 XPS 文档事件使用的常量。

```cpp
//
// structures used in XPS Document events
//
 
typedef enum
    {
        kPropertyTypeString = 1,
        kPropertyTypeInt32,
        kPropertyTypeInt64,
        kPropertyTypeByte,
        kPropertyTypeTime,
        kPropertyTypeDevMode,
        kPropertyTypeSD,
        kPropertyTypeNotificationReply,
        kPropertyTypeNotificationOptions,

    } EPrintPropertyType;

    typedef struct
    {
        EPrintPropertyType       ePropertyType;
        union
        {
            BYTE                 propertyByte;
            PWSTR                propertyString;
            LONG                 propertyInt32;
            LONGLONG             propertyInt64;
            struct {
                DWORD  cbBuf;
                LPVOID pBuf;
            }                    propertyBlob;
        } value;

    }PrintPropertyValue;

    typedef struct
    {
        WCHAR*                  propertyName;
        PrintPropertyValue      propertyValue;

    }PrintNamedProperty;

    typedef struct
    {
        ULONG                   numberOfProperties;
        PrintNamedProperty*     propertiesCollection;

    }PrintPropertiesCollection;
```

前面的代码示例中的结构 Winspool.h 中定义。

以下转义码 Winddiui.h 中定义。

```cpp
//
 // Escape code for XPS Document events
//
#define DOCUMENTEVENT_QUERYFILTER                                     14
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRE                 1
// DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRE must have same value as //DOCUMENTEVENT_CREATEDCPRE for Winspool.drv to query the driver for supported events and reset the cached events.
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRE                         2
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRE        3                           
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPOST                            4
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPOST                        5
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPOST                13
// DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPOST must have same value as //DOCUMENTEVENT_STARTDOCPOST for Winspool.drv to signal the tray ballon that //the document is completed
#define DOCUMENTEVENT_XPS_CANCELJOB                                   6
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE      7
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRINTTICKETPRE              8
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRINTTICKETPRE                  9
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRINTTICKETPOST                 10
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRINTTICKETPOST             11
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST     12
```

 

 




