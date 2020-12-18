---
title: 组件固件更新 (CFU) 固件实现指南
description: 提供有关实现组件固件更新 (CFU) 协议以及创建要安装在目标设备上的新固件映像的详细指南。
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 43178020754bbf528dfa2ed5fcc585dd03c48f80
ms.sourcegitcommit: 170bf8fc2cb5b99bc09616f59180adf72b2e5d26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "97611759"
---
# <a name="component-firmware-update-cfu-firmware-implementation-guide"></a>组件固件更新 (CFU) 固件实现指南

组件固件更新 (CFU) 是协议和用于提交要安装在目标设备上的新固件映像的过程。

> [!NOTE]
> CFU 在 Windows 10 中提供，版本 2004 (Windows 10 2020 更新) 及更高版本。

CFU 提交到常驻固件是文件对，一个文件是产品/服务部分，另一个文件是内容部分。 每个 CFU 提交 (每个产品/服务和内容对) 需要在提交发送到实现 CFU 过程的固件之前脱机创建。

在 GitHub 上的 CFU 存储库中的示例 [固件](https://github.com/Microsoft/CFU/tree/master/Firmware) 源代码中，CFU 的常规实现的通用代码包含在中 `ComponentFwUpdate.c` 。 所有其他文件都是帮助程序文件，可以对其进行更新或修改，使其成为开发人员的唯一实现。

## <a name="contents"></a>目录

- [产品/服务和内容部分](#the-offer-and-content-parts)
  - [提供注册详细信息](#offer-register-details)
  - [处理产品/服务](#processing-offers)
    - [解释提议](#interpreting-the-offer)
      - [步骤 1-检查银行](#step-1---check-bank)
      - [步骤 2-检查 hwVariantMask](#step-2---check-hwvariantmask)
      - [步骤 3-检查固件版本](#step-3---check-firmware-version)
      - [步骤 4-接受提议](#step-4---accept-offer)
  - [处理内容](#process-the-content)
    - [Content 命令的结构](#the-structure-of-the-content-command)
    - [第一个块](#the-first-block)
    - [除第一个或最后一个以外的其他任何块](#any-other-block-except-first-or-last)
    - [最后一个块](#the-last-block)
    - [最后一个块后清理](#clean-up-after-last-block)
  - [已检查强制重置](#forced-reset-checked)

## <a name="the-offer-and-content-parts"></a>产品/服务和内容部分

产品/服务和内容构成了 CFU 架构中的一对文件。

产品/服务部分只是一个16字节长的文件，用于映射到下面所述的 FWUPDATE_OFFER_COMMAND 结构。  

内容部分（要更新的实际固件采用最终用户开发人员指示的格式）。  提供的 CFU 示例代码使用 SREC 文件来查看固件内容。

产品/服务是16字节序列。  此产品/服务结构放入了产品/服务文件中。  它实质上是二进制数据而不是文本，因为该产品/服务包含特定含义的位域。

文件中表示的产品/服务映射到此 C 结构：

```cpp
typedef struct
{
   struct
   {
       UINT8 segmentNumber;
       UINT8 reserved0 : 6;
       UINT8 forceImmediateReset : 1;
       UINT8 forceIgnoreVersion : 1;
       UINT8 componentId;
       UINT8 token;
   } componentInfo;

   UINT32 version;
   UINT32 hwVariantMask;
   struct
   {
       UINT8 protocolRevision : 4;
       UINT8 bank : 2;
       UINT8 reserved0 : 2;
       UINT8 milestone : 3;
       UINT8 reserved1 : 5;
       UINT16 productId;
   } productInfo;

} FWUPDATE_OFFER_COMMAND;
```

从低到高地址，该产品/服务的第一个字节是段号。

```text
  <------- 4 bytes -----------> <-- 8 bytes -->  <-------- 4 bytes --------->
+================================-=============================================+
|  15:0 7:3  2:0  7:6  5:4  3:0   31:0   31:0     7:0  7:0  7:7  6:6  5:0  7:0 |
|  PI | R1 | MS | R0 | BK | PR  | VM   | VN   |   TK | CI | FV | FR | R0 | SN  |
+================================-=============================================+
```

从高地址到低地址：

```text
Byte(s)    Value
---------------------------------------------------------
15:14   |  (PI)  Product ID is 2 bytes
13      |  (R1)  Reserved1 5-bit register
        |  (MS)  Milestone 3-bit register
12      |  (R2)  Reserved2 2-bit register
        |  (BK)  Bank 2-bit register
        |  (PR)  Protocol Revision  2-bit register
11:8    |  (VM)  Hardware Variant Mask 32-bit register
7:4     |  (VN)  Version 32-bit register
3       |  (TK)  Token byte 8-bit register
2       |  (CI)  Component ID 8-bit register
1       |  (FV)  Force version bit  1-bit register
        |  (FR)  Force Immediate Reset  1-bit register
        |  (R0)  Reserved0 6-bit register
0       |  (SN)  Segment Number 8-bit register
---------------------------------------------------------
```

### <a name="offer-register-details"></a>提供注册详细信息

产品 ID。 此 CFU 映像的唯一产品 ID 值可以应用于该字段。

```cpp
UINT16 productID;  
```

产品/服务的内容所代表的固件里程碑。 里程碑可能是不同版本的硬件生成，例如 EV1 生成、EV2 生成等。 里程碑定义和值分配留给开发人员。

```cpp
UINT8 milestone : 3;
```

如果固件适用于特定银行-2 位域支持四个银行。   使用银行注册的格式包含在产品/服务的格式中，因为在此情况下，目标设备使用的是存款固件区域。

如果是这种情况，并且该产品/服务旨在更新正在使用的银行，则在目标上实现 CFU 的固件可能会拒绝该产品/服务。  否则，实现 CFU 的目标上的固件可执行其他操作。

如果固件映像的银行不在最终用户固件设计中，则可以忽略此字段 (设置为任何方便的值，但 bank 字段中的值是可选的，具体取决于目标固件实现 CFU) 的方式。

```cpp
UINT8 bank : 2;
```

使用的 CFU 协议的协议版本为4位。

```cpp
UINT8 protocolRevision : 4;
```

与此固件映像可在其上操作的所有唯一 HW 相对应的位掩码。 例如，该产品/服务可能表示它可在 verX 的硬件上运行，但不能在很大的硬件上运行。 位定义和值分配留给开发人员。

```cpp
UINT32 hwVariantMask;
```

提供的固件版本。

```cpp
UINT32 version;
```

一个字节标记，用于标识提供产品/服务的用户特定软件。 这旨在区分两个驱动程序和工具，两者都可以尝试更新同一正在运行的固件。 例如，可以为 CFU 更新驱动程序分配令牌0xA，并可以为0xB 分配一个开发更新工具。 现在，运行中的固件可根据尝试更新命令的进程，有选择地接受或忽略命令。

```cpp
UINT8 token;
```

设备中要应用固件更新的组件。

```cpp
UINT8 componentId;
```

产品/服务解释标志：如果想要原位固件中的版本不匹配 (旧) ，请将该位设置为强制忽略版本。

```cpp
UINT8 forceIgnoreVersion: 1;
```

强制立即重置是通过一位来断言的。  如果此位被断言，主机软件会要求原位固件中的设备执行重置。  重置操作是特定于平台的。  设备的固件可以选择执行操作，该操作将交换银行，使新更新的固件在原位固件中处于活动状态。  否则为。  它将留给固件的实现。 通常情况下，如果强制立即重置被断言，则设备将执行任何必要的操作，以使固件更新新的银行成为在目标设备上运行的活动固件。

```cpp
UINT8 forceImmediateReset : 1;
```

如果产品/服务和内容对的内容部分涉及多个内容部分。

```cpp
UINT8 segmentNumber;
```

### <a name="processing-offers"></a>处理产品/服务

ProcessCFWUOffer API 接受两个参数：

```cpp
void ProcessCFWUOffer(FWUPDATE_OFFER_COMMAND* pCommand,
                     FWUPDATE_OFFER_RESPONSE* pResponse)
```

在此用例中，假设用户软件将数据字节发送到正在运行的固件，则第一条消息是提供消息。

"产品/服务" 消息是上文所述的16字节消息 (FWUPDATE_OFFER_COMMAND 结构) 。

该服务消息是正在运行的固件用于处理产品/服务的数据。

在对产品/服务的处理过程中，正在运行的固件将通过填充结构中的字段来通知发件人 `FWUPDATE_OFFER_RESPONSE` 。

#### <a name="interpreting-the-offer"></a>解释提议

正在运行的固件应跟踪它在 CFU 过程中的状态。 它可能在 CFU 事务中间或等待在活动/非活动固件之间交换银行时，准备好/等待接受产品/服务。

如果正在运行的固件处于 CFU 事务的中间，则不接受/处理此优惠并相应地通知主机。

```cpp
   if (s_currentOffer.updateInProgress)
   {
       memset(pResponse, 0, sizeof (FWUPDATE_OFFER_RESPONSE));

       pResponse->status = FIRMWARE_UPDATE_OFFER_BUSY;
       pResponse->rejectReasonCode = FIRMWARE_UPDATE_OFFER_BUSY;
       pResponse->token = token;
       return;
   }
```

产品/服务的 "组件 ID" 字段可用于向正在运行的固件发出信号，指出从正在运行的固件请求了特殊操作。 在 CFU 代码示例中，主机使用特殊的 "产品/服务" 命令来检索 CFU 引擎的状态-无论正在运行的软件是否能够接受 CFU 产品/服务。

```cpp
   else if (componentId == CFU_SPECIAL_OFFER_CMD)
   {
       FWUPDATE_SPECIAL_OFFER_COMMAND* pSpecialCommand =
           (FWUPDATE_SPECIAL_OFFER_COMMAND*)pCommand;
       if (pSpecialCommand->componentInfo.commandCode == CFU_SPECIAL_OFFER_GET_STATUS)
       {
           memset(pResponse, 0, sizeof (FWUPDATE_OFFER_RESPONSE));

           pResponse->status = FIRMWARE_UPDATE_OFFER_COMMAND_READY;
           pResponse->token = token;
           return;
       }
   }
```

最后，如果有银行交换处于挂起状态，则进行检查。  银行交换指的是，如果该固件仍处于从运行的活动应用程序切换到新下载映像的过程中，则保留该信息。  

银行切换的执行方式和位置是嵌入式固件的特定于实现的任务。  CFU 协议和进程允许在运行 CFU 的远程用户应用程序和运行的原位固件之间交换信息。

```cpp
   else if (s_bankSwapPending)
   {
       memset(pResponse, 0, sizeof (FWUPDATE_OFFER_RESPONSE));

       pResponse->status = FIRMWARE_UPDATE_OFFER_REJECT;
       pResponse->rejectReasonCode = FIRMWARE_UPDATE_OFFER_SWAP_PENDING;
       pResponse->token = token;
       return;
   }
```

最后，如果正在运行的固件的状态不是 "忙碌"，并且该组件不是特殊命令，并且没有任何银行交换处于挂起状态，则我们可以处理此产品/服务。

处理产品/服务涉及但并不局限于下面列出的四个步骤：

##### <a name="step-1---check-bank"></a>步骤 1-检查银行

在产品/服务中，将正在运行的应用程序的银行检查到银行。  它们是相同还是不同？

如果相同，则拒绝该产品/服务 (我们不想覆盖正在运行/活动的映像) 。

否则继续。

##### <a name="step-2---check-hwvariantmask"></a>步骤 2-检查 hwVariantMask

正在运行的固件 `hwVariantMask` 会根据其运行所在的硬件检查该产品/服务中的。  如果产品/服务对目标无效，则这允许嵌入式固件拒绝产品/服务。 （例如： 如果正在运行的固件位于旧的硬件版本上，而新提供的固件适用于较新的 HW 版本，则正在运行的固件应拒绝此提议) 

如果无效，则拒绝该产品/服务。

否则继续。

##### <a name="step-3---check-firmware-version"></a>步骤 3-检查固件版本

检查提供的固件内容版本是否与当前应用程序固件版本相同或更高。

用户实现留给用户实现来决定如何检查哪个固件大于另一个固件，以及是否允许使用产品/服务的 "forceIgnoreVersion" 字段。 典型的固件开发将允许在产品开发和固件的调试版本中使用 "forceIgnoreVersion" 字段，但不允许 (不允许在产品/发行固件) 更新旧固件。

如果此检查失败，则拒绝该产品/服务。

否则继续。

##### <a name="step-4---accept-offer"></a>步骤 4-接受提议

产品/服务非常好。  接受该产品/服务，其中包含针对固件向远程用户应用程序返回消息和状态的方式的响应。 所谓的 "响应" 是 (打包的数据结构的数据，如演示标头文件) 中所示，此数据由设备的相应方法写出到用户应用程序。

### <a name="process-the-content"></a>处理内容

内容的处理通常是一个多步骤过程。 多个步骤是指固件的功能，该功能接受部分（也称为 "块"）的固件映像。  将整个图像同时发送到嵌入的固件并不总是可行的，因此，实现 CFU 协议和过程以在小部分中接受内容是现实的。

此讨论在描述 CFU 内容的过程时，将使用 tha 假设。

内容处理的状态机包含三种状态。

1. 处理第一个块的状态。

1. 处理最后一个块的状态。

1. 在第一个和最后一个之间处理任何块的状态。

#### <a name="the-structure-of-the-content-command"></a>Content 命令的结构

与产品/服务一样，内容具有一个结构，其中包含 CFU 算法在演示中使用的字段。

```cpp
typedef struct
{
   UINT8 flags;
   UINT8 length;
   UINT16 sequenceNumber;
   UINT32 address;
   UINT8 pData[MAX_UINT8];
} FWUPDATE_CONTENT_COMMAND;
```

Content 命令的结构比提供结构简单。 内容定义为要写入内存中的字节序列。  内容的引言是此结构的字段：

1. `UINT8 flags`   表示内容 "块" 是第一个、最后一个还是另一个。

1. `UINT8 length`  标记字段的长度 `pData` 。  在 CFU 的演示代码中，的大小限制 `pData` 为255字节。  其他实现可能会改变 "块" 的最大大小。

1. `UINT16 sequenceNumber`  将正在提交的块的索引计数器标记为内容。

1. `UINT32 address`  块的地址偏移量。  在此版本 CFU 的演示中，实现提供了有关每个应用区域的物理地址的预定义信息。  例如，两个银行固件实现可能 App1 从 address 开始 `0x9000` ，并从地址开始 App2 `0xA0000` 。 因此，根据固件映像的准备方式 (S-记录) SREC 中的地址可以是物理地址，也可以是偏移量。  在任何情况下，都需要在准备内容和实现的 CFU 内容处理的特定例程之间进行共享理解，以确定在内存中写入块的实际物理地址。  对于每个内容博客，固件开发人员都可以采用最佳做法并检查有效的地址范围。 例如，CFU 代码演示了如果可能 App1 (`0x9000` 表示) 有与 App2 等重叠的地址，则进行检查。

1. `UINT8 pData[MAX_UINT8]` -这是固件映像块的原始字节。  在用户应用程序中执行的操作仅将 `length` 字节放入内容块的完整字节流中。  

根据提供的代码中的 CFU 演示，内容结构中没有任何位域。

#### <a name="the-first-block"></a>第一个块

第一个块开始下载固件内容。  运行的固件尝试将块写入到非易失性内存。  当然，内容 "块" 包含有关应将块写入内存中的位置、要写入的数据量以及其他字段的信息。

每个组件名目标设备不同，有多种方法可将数据保存到内存中。 例如，一个组件 Id 可能需要写入内部闪存，另一个组件可能会写入外部 SPI 闪存，另一个组件可能会利用另一个 IC 协议来更新它的映像。 本文档中包含的演示重点介绍了如何使用一个函数， `ICompFwUpdateBspWrite` 每个唯一的固件必须实现该函数，并了解其设计目标的基础非易失性内存 i/o 函数。

#### <a name="any-other-block-except-first-or-last"></a>除第一个或最后一个以外的其他任何块

如果用户应用程序提供另一个块，并再次将消息中的元数据用于要写入的块的地址、包含的字节数以及其他字段，则接受新块的过程将继续。

与第一个块方案一样，中原位固件会将其视为。

不过，应注意，在任何时候，系统无法捕获块并将其保存到内存中，原位固件中的响应失败代码。  

#### <a name="the-last-block"></a>最后一个块

仅当原位固件需要执行任务来验证刚写入内存的映像时，最后一个块才会出现问题。

首先，最后一个块写入内存。

然后，至少应在已写入内存的数据之间进行 CRC 检查， (从第一个块到最后一个块) 与最后一个块中的 CRC 字段进行比较。 它留给每个实现固件来了解如何获取已下载映像的 CRC。

请记住，执行 CRC 检查确实会耗费时间。 与 CFU 的正常执行流不同，后者用于提议和阻止提交。  如果最后一个块提交（如果它包括 CRC 检查），则只涉及到 CRC 检查可能检查大型内存区域这一事实，只涉及到一定的延迟。  根据目标设备和其他因素，这可能不是问题。

> [!IMPORTANT]
> 传入映像的 CRC 检查是可选的，可能会被注释掉。但是，最佳实践应投入到最少采用此检查。 强烈建议在 CFU 过程中的这一点，执行其他操作以确保已下载映像的完整性。 其中一些操作可能包括验证映像的 "已签名" 部分和/或检查信任的证书链或确保安全固件映像的其他最佳做法方法。 它们留给固件开发人员。

#### <a name="clean-up-after-last-block"></a>最后一个块后清理

现在，最后一个块已写入，CRC 检查完成后，如果验证的任何部分失败，固件可能会发生故障。

否则，预期是固件中的 CFU 进程将响应成功状态。

### <a name="forced-reset-checked"></a>已检查强制重置

产品/服务中的强制重置标志用于确定目标的 MCU 是否应重置 (用户定义的重置) 。

通常，当强制重置时，目的是使 MCU 执行重置，以便使应用程序 bank 切换。 更新持久性变量以指示要在重置时启动的固件映像留给固件开发人员。
