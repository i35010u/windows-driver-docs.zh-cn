---
title: XPS 驱动程序文档事件
description: XPS 驱动程序文档事件
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv，事件
- 事件 WDK XPSDrv
- 通知 WDK XPSDrv
- DrvDocumentEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faef2ee75eb6073fb678f8a48513a9a95d17d011
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785745"
---
# <a name="xps-driver-document-events"></a>XPS 驱动程序文档事件


Microsoft Windows Presentation Foundation (WPF) 打印支持在文档假脱机期间发送 XPSDrv 打印驱动程序通知事件，类似于 GDI 打印支持如何向 GDI 打印驱动程序发送通知。 WPF 打印支持还使用 GDI 打印支持所使用的相同的 **DrvDocumentEvent** DDI 函数，但定义了新的事件以支持 XPS 文档处理事件。 GDI 打印支持将继续向基于 GDI 的打印驱动程序和用于 Microsoft Win32 应用程序打印的 XPSDrv 打印驱动程序发出 **DrvDocumentEvent** 事件处理程序。

### <a name="drvdocumentevent-event-handler-overview"></a>DrvDocumentEvent 事件处理程序概述

如有必要，XPSDrv 打印驱动程序可以从配置模块中导出 **DrvDocumentEvent** 事件处理程序，以截获文档处理函数。 新的 XPS 文档相关事件由以 "DOCUMENTEVENT XPS" 开头的符号名称标识 \_ \_ 。

WPF 打印支持调用 XPSDrv 打印驱动程序的 **DrvDocumentEvent** 函数，同时对文档进行后台打印以便打印。 每次调用发生在过程中的不同步骤。 每个调用的处理步骤由 *iEsc* 参数的值标识。 *PvIn* 和 *pvOut* 参数引用的缓冲区内容会有所不同，具体取决于处理步骤。

本主题中的以下小节仅介绍 WPF 打印支持生成的 XPS 文档处理事件。

### <a name="drvdocumentevent-event-handler-description"></a>DrvDocumentEvent 事件处理程序描述

**DrvDocumentEvent** 事件处理程序具有以下调用格式。 本节中的代码和参数定义仅用于信息。

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

### <a name="parameters"></a>参数

<a href="" id="hprinter"></a>*hPrinter*  
WPF 打印支持提供的打印机句柄。

<a href="" id="hdc"></a>*hdc*  
调用方提供的、 **CreateDC** 调用生成的设备上下文句柄。 Microsoft Windows SDK 文档中介绍了 (**CreateDC** ) 。如果将 *IESC* 设置为 DOCUMENTEVENT CREATEDCPRE，则此参数为零 \_ 。

打印文档时，系统将为 XPS 和 GDI 文档使用相同的事件值。 驱动程序必须了解这种相似性，并根据 *hdc* 确定作业类型。 *hdc* \_ \_ 对于所有 DOCUMENTEVENT \_ XPS \_ *Xxx* 事件，hdc 等于无效的句柄值。 此检查将根据调用应用程序确定 **DrvDocumentEvent** 事件值的正确解释。 此检查仅适用于 XPSDrv 打印驱动程序。

<a href="" id="iesc"></a>*iEsc*  
调用方提供的转义代码，用于标识要处理的事件。 此参数可以是以下整数常量之一。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT \_ QUERYFILTER   
WPF 打印支持发送此事件以查询打印驱动程序，以获取驱动程序将响应的 XPS 文档处理事件的列表。 此事件在任何其他 XPS 文档相关事件之前发出。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRE  
WPF 打印支持会在将 FixedDocumentSequence 添加到 XPS 假脱机文件之前发送此事件。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPOST  
WPF 打印支持会在将 FixedDocumentSequence 添加到 XPS 假脱机文件后发送此事件。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRE  
WPF 打印支持会在将 FixedDocument 添加到 XPS 假脱机文件之前发送此事件。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPOST  
WPF 打印支持在将 FixedDocument 添加到 XPS 假脱机文件后发送此事件。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
WPF 即将向 FixedDocumentSequence (作业级别添加 PrintTicket) 。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST  
WPF 应在相应的 **DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE** 事件上释放驱动程序返回的 datathat。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPRE  
WPF 即将向 FixedDocument (文档级别添加 PrintTicket) 。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPOST  
WPF 应释放驱动程序在相应的 DOCUMENTEVENT \_ XPS ADDFIXEDDOCUMENTPRINTTICKETPRE 事件上返回的数据 \_ 。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPRE  
WPF 即将向 FixedPage (页面级别添加 PrintTicket) 。

<a href="" id="documentevent-xps-addfixedpageprintticketpost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPOST  
WPF 释放驱动程序在相应的 DOCUMENTEVENT \_ XPS ADDFIXEDPAGEPRINTTICKETPRE 事件上返回的数据 \_ 。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT \_ XPS \_ CANCELJOB  
WPF 打印支持在调用 "取消作业" 操作之前发送此事件。

<a href="" id="documentevent-xps-commitjob"></a>DOCUMENTEVENT \_ XPS \_ COMMITJOB  
WPF 已完成将日期写入当前文件的操作。

<a href="" id="cbin"></a>*cbIn*  
*Pvln* 参数引用的缓冲区的大小（以字节为单位）。 此值由 WPF 打印支持提供，并由事件处理程序读取。

<a href="" id="pvin"></a>*pvIn*  
调用方提供的指针。 此参数的使用取决于 *iEsc* 值，如下表所述。  (\_ \_ 此列表中未显示的 DOCUMENTEVENT XPS *Xxx* 事件，则不会使用 *pvIn* 。 ) 

<a href="" id="documentevent-queryfilter"></a>DOCUMENTEVENT \_ QUERYFILTER  
*pvIn* 指向与 \_ DOCUMENTEVENT QUERYFILTER)  (相同的 PDOCEVENT 筛选器结构 \_ 。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含三个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。 EscapeCode 是事件值。

-   JobIdentifier，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。 JobIdentifier 是调用 GetJob ( # A1 和 **SetJob** ( # A3 所需的 ID。

-   JobName，它是 EPrintPropertyType：： kPropertyTypeString (UNICODE) 值。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPOST  
与 DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRE 相同。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含两个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。 EscapeCode 是事件值。

-   DocumentNumber，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPOST  
与 DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRE 相同。

<a href="" id="documentevent-xps-addfixedpagepre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含两个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。

-   PageNumber，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。

<a href="" id="documentevent-xps-addfixedpagepost"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPOST  
与 DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRE 相同。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含四个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 。 EscapeCode 是事件值。

-   JobIdentifier，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。

-   JobName，它是 EPrintPropertyType：： kPropertyTypeString (UNICODE) 值。

-   PrintTicket，它是 EPrintPropertyType：： kPropertyTypeByte 值。

你必须在 "PRE" 事件上分配 PrintPropertiesCollection 结构及其属性，并在相应的 "POST" 事件上将其释放。 你可以将 *pvOut* 设置为 **NULL** ，以指示你支持该事件，但不会对更改给定文档或页面的 PrintTicket 感兴趣。 插件决不应在 "PRE" 和 "POST" 事件之间卸载。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
*pvIn* 与 DOCUMENTEVENT \_ XPS ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE 中的 pvOut 相同 \_

驱动程序必须释放 *pvIn*。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含三个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。 EscapeCode 是事件值。

-   DocumentNumber，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。

-   PrintTicket，它是 EPrintPropertyType：： kPropertyTypeByte 值。

你必须在 "PRE" 事件上分配 PrintPropertiesCollection 结构及其属性，并在相应的 "POST" 事件上将其释放。 你可以将 *pvOut* 设置为 **NULL** ，以指示你支持该事件，但不会对更改给定文档或页面的 PrintTicket 感兴趣。 插件决不应在 "PRE" 和 "POST" 事件之间卸载。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPOS  
*pvIn* 与 DOCUMENTEVENT XPS ADDFIXEDDOCUMENTPRINTTICKETPRE 中的 *pvOut* 相同 \_ \_ 。

驱动程序必须释放 *pvIn*。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPRE  
*pvIn* 指向 PrintPropertiesCollection 结构 (参阅包含三个属性的 winspool.drv) ：

-   EscapeCode，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 值。 EscapeCode 是事件值。

-   PageNumber，它是 EPrintPropertyType：： kPropertyTypeInt32 (ULONG) 。

-   PrintTicket，它是 EPrintPropertyType：： kPropertyTypeByte。

你必须在 "PRE" 事件上分配 PrintPropertiesCollection 结构及其属性，并在相应的 "POST" 事件上将其释放。 你可以将 *pvOut* 设置为 **NULL** ，以指示你支持该事件，但不会对更改给定文档或页面的 PrintTicket 感兴趣。 插件决不应在 "PRE" 和 "POST" 事件之间卸载。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPOS  
*pvIn* 与 DOCUMENTEVENT XPS ADDFIXEDPAGEPRINTTICKETPRE 中的 *pvOut* 相同 \_ \_ 。

驱动程序必须释放 *pvIn*。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT \_ XPS \_ CANCELJOB  
*pvIn* 为 **NULL**。

<a href="" id="cbout"></a>*cbOut*  
如果 *iEsc* 参数包含 **DOCUMENTEVENT \_ QUERYFILTER**，则 WPF 打印支持提供 *pvOut* 参数在 *cbOut* 参数中引用的缓冲区大小。 对于 *iEsc* 的所有其他值，不使用 *cbOut* 。

<a href="" id="--------pvout"></a> pvOut  
指向 WPF 打印支持所提供的缓冲区的指针。 缓冲区大小和内容取决于 *iEsc* 参数的值。 以下列表描述了每个 *iEsc* 值的 *pvOut* 缓冲区的内容。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT \_ QUERYFILTER   
调用方提供的指向包含 DOCEVENT 筛选器结构的缓冲区的指针 \_ 。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre-"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE   
指向 PrintPropertiesCollection 结构的指针 (参阅 Winspool.drv) ，其中包含类型为 EPrintPropertyType：： kPropertyTypeBuffer 的 "PrintTicket" 属性。 此属性始终存在。 如果没有可用的 PrintTicket，则 PrintPropertyValue 的值为 **NULL**。

属性包含 XML PrintTicket，Microsoft Windows Presentation Foundation (WPF) 将使用 PrintTicket，而不是 **system.windows.xps.xpsdocumentwriter>** 调用方提供的。  (如果 *pvOut* 为 **null** 或属性不存在，或者属性数据为 **null**，则 WPF 使用调用方提供的 PrintTicket。 ) 

处理此事件之后，WPF 将调用 **DocumentEvent** ，并将 DocumentEvent \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST 用于驱动程序发布 *pvOut*。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPRE  
指向 PrintPropertiesCollection 结构的指针 (参阅 Winspool.drv) ，其中包含 EPrintPropertyType：:P ropertyTypeBuffer 类型的 "PrintTicket" 属性。 Thisproperty 始终存在。 如果没有可用的 PrintTicket，则 **PrintPropertyValue** 的值为 **NULL**。

属性包含 XML PrintTicket，WPF 将使用 PrintTicket，而不是 **system.windows.xps.xpsdocumentwriter>** 调用方提供的类型。  (如果 *pvOut* 为 **null** 或属性不存在，或者属性数据为 **null**，则 WPF 使用调用方提供的 PrintTicket。 ) 

处理此事件之后，WPF 将调用 **DocumentEvent** ，并将 DocumentEvent \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPOST 用于驱动程序发布 *pvOut*。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDDOCUMENTPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPRE  
指向 PrintPropertiesCollection 结构的指针 (参阅 Winspool.drv) ，其中包含类型为 EPrintPropertyType：： PropertyTypeBuffer 的 "PrintTicket" 属性。 此属性始终存在。 如果没有可用的 PrintTicket，则 **PrintPropertyValue** 的值为 **NULL**。

属性包含 XML PrintTicket，WPF 将使用 PrintTicket，而不是 **system.windows.xps.xpsdocumentwriter>** 调用方提供的类型。  (如果 *pvOut* 为 **null** 或属性不存在，或者属性数据为 **null**，则 WPF 使用调用方提供的 PrintTicket。 ) 

处理此事件之后，WPF 将调用 **DocumentEvent** ，并将 DocumentEvent \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPOST 用于驱动程序发布 *pvOut*。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT \_ XPS \_ ADDFIXEDPAGEPRINTTICKETPOS  
**NULL**

### <a name="return-value"></a>返回值

**DrvDocumentEvent** 返回以下值之一：

<a href="" id="documentevent-success"></a>DOCUMENTEVENT \_ 成功  
驱动程序已成功处理 *iEsc* 标识的转义代码。

<a href="" id="documentevent-failure"></a>DOCUMENTEVENT \_ 失败  
驱动程序支持 *iEsc* 标识的转义代码，但发生了错误。

<a href="" id="documentevent-unsupported"></a>\_不支持 DOCUMENTEVENT  
该驱动程序不支持 *iEsc* 标识的转义码。

### <a name="xps-document-event-structures-and-event-code-values"></a>XPS 文档事件结构和事件代码值

下面的代码示例演示了新的 XPS 文档事件使用的结构和常量。

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

前面的代码示例中的结构在 Winspool.drv 中定义。

以下转义代码在 Winddiui 中定义。

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

 

 




