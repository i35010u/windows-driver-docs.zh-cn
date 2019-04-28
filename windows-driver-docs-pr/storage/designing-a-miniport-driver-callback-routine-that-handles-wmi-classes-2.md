---
title: 设计微型端口驱动程序回调例程来处理 WMI 类
description: 设计可以通过方法处理 WMI 类的微型端口驱动程序回调例程
ms.assetid: f5a0331a-1daa-4ef5-bf99-14b3a3393956
keywords:
- WMI Srb WDK 存储，设计回调例程
- 回调例程 WDK WMI Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8114a2b9aa0a79d9bdd529605055a07a95494bb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331739"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-methods"></a>设计可以通过方法处理 WMI 类的微型端口驱动程序回调例程


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


本部分中使用的示例包含 WMI 方法的 WMI 类，并介绍相应的微型端口驱动程序回调例程应如下所示。 有关执行 WMI 方法的微型端口驱动程序回调例程的详细信息，请参阅[ **HwScsiWmiExecuteMethod**](https://msdn.microsoft.com/library/windows/hardware/ff557332)。

以下示例中 WMI 类包含 WMI 方法：

```cpp
class MSFC_HBAAdapterMethods
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetDiscoveredPortAttributes(
            [in ] uint32 PortIndex,
            [in ] uint32 DiscoveredPortIndex,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
    [
     Implemented,
     WmiMethodId(2)
    ]
    void GetPortAttributesByWWN(
            [in, HBAType("HBA_WWN")] uint8 wwn[8],
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
          [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
};
class MSFC_HBAFCPInfo
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetFcpTargetMapping(
            [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
            [in ] uint32 InEntryCount,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out] uint32 TotalEntryCount,
            [out] uint32 OutEntryCount,
            [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry  
                 Entry[]
            );
};
```

**MSFC\_HBAAdapterMethods**类包含两个方法**GetDiscoveredPortAttributes**并**GetPortAttributesByWWN**。 MSFC\_HBAFCPInfo 类包含一种方法， **GetFcpTargetMapping**。

SCSI 端口 WMI 库调度例程调用微型端口驱动程序时执行方法的回调例程，它将传入*GuidIndex*值，该值标识 WMI 类*MethodId*值标识在类中，方法和一个*InstanceIndex*值，该值标识其可能的类来处理多个实例。 回调例程应采取相应的措施的类、 方法和类实例的任意给定组合。

下面的示例演示 execute 方法回调例程可能会如何处理在上一示例中的方法。

```cpp
HwScsiWmiExecuteMethod (
    IN PVOID Context,
    IN PSCSIWMI_REQUEST_CONTEXT DispatchContext,
    IN ULONG GuidIndex,
    IN ULONG InstanceIndex,
    IN ULONG MethodId,
    IN ULONG InBufferSize,
    IN ULONG OutBufferSize,
    IN OUT PUCHAR Buffer
    )

  switch(GuidIndex) { 
    case MSFC_HBAAdapterMethodsGuidIndex:
    {
      switch(MethodId) {
      case GetDiscoveredPortAttributes:
        // handle method here 
        Switch(InstanceIndex) {
        case 1:
          // handle instance 1
          PGetDiscoveredPortAttributes_IN In;
          PGetDiscoveredPortAttributes_OUT Out;
          // note: input and output parameters use the same buffer
          In = (PGetDiscoveredPortAttributes_IN)Buffer;
          Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
          // put code for method here
          break;
        case 2:
       // handle instance 2
        default:
          break;
        }
      case GetPortAttributesByWWN:
        // handle method here 
      default:
        break;
    }
    case MSFC_HBAFCPInfoGuidIndex:
    {
      switch(MethodId) {
      case GetFcpTargetMapping:
        // handle method here 
      default:
        break;
      }
    }
```

WMI 工具套件 (**mofcomp**并**wmimofck**) 简化了编写此例程通过自动生成的二进制类型库和每个 wmi 定义符号常量的标头文件的任务类 GUID 索引和每个方法标识符。 有关如何使用这些工具的详细信息，请参阅[编译的驱动程序的 MOF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542012)并[使用 wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)。

**Wmimofck**工具生成的.bmf 二进制文件从生成的.h 文件**mofcomp**。 通过连接到 WMI 类的名称的"GuidIndex"后缀来构成类索引的符号常量的名称。 例如，使用**MSFC\_FibrePortHBAMethods**类，该工具将创建名为符号常量**MSFC\_FibrePortHBAMethodsGuidIndex**表示GUID 为该类的的索引。 在类似的方式，该工具将使用到窗体符号常量表示的方法，而无需添加任何后缀的方法名称。 该方法的名称的符号常量是只需方法的名称。 在示例中，switch 语句测试方法标识符的值。 在 switch 语句中的每个用例对应于方法名称。

若要定义的 WMI 类方法所使用的 MOF 语法类似于例程;但是，WMI 方法不是一个例程。 当**mofcomp**并**wmimofck**工具处理在 MOF 文件中的方法定义，它们会产生两个单独 C 语言结构声明的方法。 一个结构是在 MOF 中标识的参数文件作为输入的参数"\[中\]"前缀和另一个结构标识为输出参数的参数"\[出\]"前缀。

**Wmimofck**工具窗体包含方法的结构的名称的输入参数连接在一起的后缀"\_IN"为方法的名称。 例如，如果该方法的名称是**GetDiscoveredPortAttributes**， **wmimofck**会自动生成名为 GetDiscoveredPortAttributes 结构声明\_in。 同样， **wmimofck**生成的声明的名为 GetDiscoveredPortAttributes 结构\_保存方法的输出参数的扩展。

以下代码片段演示如何执行方法回调例程无法验证调用的方法的输入和输出缓冲区的大小**GetDiscoveredPortAttributes**在一个名为类**MSFC\_HBAPortMethods**:

```cpp
case MSFC_HBAPortMethodsGuidIndex:
  switch(MethodId) {
    case GetDiscoveredPortAttributes:
  {
      BOOLEAN bInputBigEnough = (InBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_IN))
      BOOLEAN bOutputBigEnough = (OutBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_OUT))
      if (bInputBigEnough && bOutputBigEngough) {
        PGetDiscoveredPortAttributes_IN In;
        PGetDiscoveredPortAttributes_OUT Out;

        In = (PGetDiscoveredPortAttributes_IN)Buffer;
         Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
        // 
        // process method here
      //
        status = SRB_STATUS_SUCCESS;
      } else {
        status = SRB_STATUS_DATA_OVERRUN;
      }
    }
```

返回前，应调用回调例程[ **ScsiPortWmiPostProcess**](https://msdn.microsoft.com/library/windows/hardware/ff564796)。 此 SCSI 端口 WMI 库例程的信息，例如请求的状态和返回数据的大小更新请求上下文。 有关存储的请求上下文中的信息的详细信息，请参阅[ **SCSIWMI\_请求\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff564946)。

 

 




