---
title: 读取和筛选调试消息
description: 读取和筛选调试消息
ms.assetid: 785469d2-30b8-4f73-b397-80bf89ed20ea
keywords:
- 读取和筛选调试消息
- 调试消息、 读取和筛选
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944f36f07f24e7bb13446a4a078e035ede976d50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521961"
---
# <a name="reading-and-filtering-debugging-messages"></a>读取和筛选调试消息


## <span id="ddk_reading_and_filtering_debugging_messages_dbg"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_DBG"></span>


内核模式代码可以使用**DbgPrintEx**并**KdPrintEx**例程来发送消息到内核调试器只传输在某些情况下。 这允许您筛选出不感兴趣的消息。

**请注意**  在 Windows Server 2003 和早期版本的 Windows， **DbgPrint**并**KdPrint**无条件地将消息发送到内核调试程序。 在 Windows Vista 和更高版本的 Windows，这些例程发送消息，有条件地，如**DbgPrintEx**并**KdPrintEx**。 使用任何版本的 Windows，建议你使用**DbgPrintEx**并**KdPrintEx**，因为这些规则可以控制在其下发送消息的条件。

 

这些例程的完整文档，请参阅 Windows 驱动程序工具包。

基本过程如下所示：

**若要筛选调试消息**

1.  对于每个你想要发送到调试器的消息，使用函数**DbgPrintEx**或**KdPrintEx**驱动程序的代码中。 合适的组件将名称传递给*ComponentId*参数和值传递到*级别*反映严重性或此消息的性质的参数。 消息本身传递给*格式*并*自变量*与作为参数**printf**。

2.  将相应的值设置*组件筛选器掩码*。 每个组件都有不同的掩码;掩码值指示要显示该组件的消息。 组件筛选器掩码可能使用注册表编辑器，在注册表中或使用内核调试程序的内存设置。

3.  将内核调试程序附加到计算机。 每次您的驱动程序将传递到一条消息**DbgPrintEx**或**KdPrintEx**，传递给的值*ComponentId*并*级别*将与相应的组件筛选器掩码的值进行比较。 如果这些值都满足特定条件，将发送到内核调试程序并显示消息。 否则，将不发送任何消息。

请遵循完整的详细信息。 此页上的所有引用**DbgPrintEx**同样适用于**KdPrintEx**。

### <a name="span-ididentifying-the-component-namespanspan-ididentifyingthecomponentnamespanidentifying-the-component-name"></a><span id="identifying-the-component-name"></span><span id="IDENTIFYING_THE_COMPONENT_NAME"></span>用于标识组件名称

每个组件都有单独的筛选器掩码。 这使调试器能够在单独配置每个组件的筛选器。

每个组件即为不同的方式，具体取决于上下文。 在中*ComponentId*的参数**DbgPrintEx**，组件名称带有前缀"DPFLTR\_"和与后缀"\_ID"。 在注册表中，组件筛选器掩码必须与组件本身相同的名称。 在调试器中，组件筛选器掩码前缀为"Kd\_"和与后缀"\_掩码"。

所有组件名称的完整列表 (在 DPFLTR\_*XXXX*\_ID 格式) 在 Microsoft Windows Driver Kit (WDK) 标头 ntddk.h 和 Windows SDK 标头 ntrtl.h 中。 大多数这些组件名称被保留的用于 Windows 和驱动程序由 Microsoft 编写。

有六个组件名称保留为独立硬件供应商。 若要避免混合驱动程序的输出与 Windows 组件的输出，应使用以下组件名称之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件名称</th>
<th align="left">驱动程序类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IHVVIDEO</strong></p></td>
<td align="left"><p>视频驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVAUDIO</strong></p></td>
<td align="left"><p>音频驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVNETWORK</strong></p></td>
<td align="left"><p>网络驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVSTREAMING</strong></p></td>
<td align="left"><p>内核流式处理驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVBUS</strong></p></td>
<td align="left"><p>总线驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVDRIVER</strong></p></td>
<td align="left"><p>任何其他类型的驱动程序</p></td>
</tr>
</tbody>
</table>

 

例如，如果你正在编写的视频驱动程序，则会使用 DPFLTR\_IHVVIDEO\_ID 作为*ComponentId*参数**DbgPrintEx**，使用值名称**IHVVIDEO**在注册表中，并参考**Kd\_IHVVIDEO\_掩码**在调试器中。

在 Windows Vista 和更高版本的 Windows 中，所有消息都发送**DbgPrint**并**KdPrint**与关联**默认**组件。

### <a name="span-idchoosingthecorrectlevelspanspan-idchoosingthecorrectlevelspanchoosing-the-correct-level"></a><span id="choosing_the_correct_level"></span><span id="CHOOSING_THE_CORRECT_LEVEL"></span>选择正确的级别

*级别*的参数**DbgPrintEx**例程是类型为 DWORD。 要使用它来确定*重要性位域*。 之间的连接*级别*参数，则此位字段上的大小取决于*级别*:

-   如果*级别*等于 0 到 31，非独占的它被解释为位移位之间的数字。 重要性位字段设置为值 1 &lt; &lt; *级别*。 因此选择介于 0 到 31 个*级别*会导致完全设置一个位的位字段。 如果*级别*为 0，则位域是等效于 0x00000001; 如果*级别*为 31，位域为等效于 0x80000000。

-   如果*级别*是介于 32 和非独占，重要性位域设置的值为 0xFFFFFFFF*级别*本身。

因此，如果你想要设置为 0x00004000 的位域，则可以指定*级别*作为 0x00004000 或只需为 14。 请注意，某些位字段值不能通过此系统-包括的位字段可能是完全为零。

以下常量也可用于设置的值*级别*。 它们在 Microsoft Windows Driver Kit (WDK) 标头 ntddk.h 和 Windows SDK 标头 ntrtl.h 定义：

```cpp
#define   DPFLTR_ERROR_LEVEL     0
#define   DPFLTR_WARNING_LEVEL   1
#define   DPFLTR_TRACE_LEVEL     2
#define   DPFLTR_INFO_LEVEL      3
#define   DPFLTR_MASK    0x8000000
```

一种简单方法使用*级别*参数是为 0 到 31-使用 bits 之间始终使用值 0、 1、 2、 3 的含义由 DPFLTR\_*XXXX*\_级别，并使用其他位来表示你选择的任何内容。

使用的另一个简单办法*级别*参数是始终使用显式的位域。 如果选择此方法时，可能需要或值 DPFLTR\_屏蔽与位域; 这可确保，不会意外地使用小于 32 的值。

若要使您的驱动程序兼容于 Windows 使用消息级别的方式，应仅设置重要性位域的最低位 (0x1) 如果发生严重错误。 如果使用的*级别*值小于 32，这对应于 DPFLTR\_错误\_级别。 如果设置此位，将您的消息，您可以的随时有人将内核调试程序附加到正在其运行您的驱动程序的计算机。

在适当情况下，应使用警告、 跟踪和信息级别。 其他位可以自由地用于任何目的，您有帮助。 这可以有各种不同的消息类型，可以有选择地显示或隐藏。

在 Windows Vista 和更高版本的 Windows 中，所有消息都发送**DbgPrint**并**KdPrint**行为类似于**DbgPrintEx**和**KdPrintEx**消息*级别*等于 DPFLTR\_信息\_级别。 换而言之，这些消息将第三个位其重要性位域的设置。

### <a name="span-idsetting-the-component-filter-maskspanspan-idsettingthecomponentfiltermaskspansetting-the-component-filter-mask"></a><span id="setting-the-component-filter-mask"></span><span id="SETTING_THE_COMPONENT_FILTER_MASK"></span>设置组件的筛选器掩码

有两种方法来设置组件筛选器掩码：

- 可在注册表项来访问组件筛选器掩码**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\调试打印筛选器**。 使用注册表编辑器，创建或打开此密钥。 在此项下所需的组件，以大写形式的名称创建一个值。 将设置为你想要使用作为组件筛选器掩码的 DWORD 值。

- 如果内核调试程序处于活动状态，它可以通过取消引用存储在符号中的地址来访问组件筛选器掩码值**Kd\_**<em>XXXX</em>**\_掩码**，其中*XXXX*是所需的组件名称。 可以在 WinDbg 或与 KD 显示此掩码的值**dd (显示 DWORD)** 命令，或输入一个新的组件筛选器掩码与**ed (输入 DWORD)** 命令。 如果符号不明确的危险，你可能会希望指定此符号作为**nt ！Kd\_**<em>XXXX</em>**\_掩码**。

存储在注册表中的筛选器掩码在启动过程才会生效。 由调试器创建的筛选器掩码会立即生效，并一直持续，直到重新启动 Windows。 在注册表中设置的值可以重写由调试器，但组件筛选器掩码将返回到如果重新启动系统注册表中指定的值。

此外，还有名为系统级掩码**WIN2000**。 这相当于 0x1 默认情况下，尽管它可以通过注册表或其他组件一样调试程序更改。 执行筛选时，每个组件筛选器掩码是与第一个或运算**WIN2000**掩码。 具体而言，这意味着的组件永远不会被其掩码指定默认值为 0x1。

### <a name="span-idcriteria-for-displayingthemessagespanspan-idcriteriafordisplayingthemessagespancriteria-for-displaying-the-message"></a><span id="criteria-for-displaying_the_message"></span><span id="CRITERIA_FOR_DISPLAYING_THE_MESSAGE"></span>用于显示消息的条件

当**DbgPrintEx**称为在内核模式代码中，Windows 消息的重要性位指定字段进行比较*级别*与由指定组件的筛选器掩码*ComponentId*.

**请注意**  回想一下，当*级别*参数为 0 到 31 之间，重要性位字段值等于 1 &lt; &lt; *级别*，但当*级别*参数为 32 个或更高版本，只需等于重要性位域*级别*。

 

Windows 执行 AND 运算的重要性位字段和组件筛选器掩码。 如果结果为非零值，该消息发送到调试器。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面是一个示例。

假定在上一次启动之前, 已创建中的以下值**调试打印筛选器**密钥：

-   **IHVVIDEO**，其值等于 DWORD 0x2

-   **IHVBUS**、 等于 DWORD 0x7FF

现在您发出内核调试程序中的以下命令：

```dbgcmd
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

在此情况下， **IHVVIDEO**组件具有 0x8、 一个筛选器掩码**IHVAUDIO**组件具有 0x7，一个筛选器掩码和**IHVBUS**组件具有 0x7FF 的筛选器掩码。

但是，因为这些掩码是自动或运算与**WIN2000**系统级掩码 （这是通常等于 0x1）， **IHVVIDEO**掩码是等效于 0x9。 实际上，其筛选器掩码的组件尚未设置根本 (例如， **IHVSTREAMING**或**默认**) 会将筛选器掩码设置为 0x1。

现在，假设以下函数调用发生在各种驱动程序：

```cpp
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

第一条消息及其*级别*参数等于 DPFLTR\_信息\_级别，这是 3。 由于这是小于 32，则将其视为移位，导致 0x8 重要性位域。 此值是然后它使用生效**IHVVIDEO**组件 0x9，给出非零结果的筛选器掩码。 因此，第一条消息将传送到调试器中。

第二个消息具有其*级别*参数等于 7。 同样，这被视为移位，导致 0x80 重要性位域。 这然后将它与**IHVAUDIO**组件 0x7，给出零结果的筛选器掩码。 因此第二条消息不会传输。

第三个消息具有其*级别*参数等于 DPFLTR\_掩码 | 0x10。 此值大于 31，并因此重要性位域设置的值相等*级别*-换而言之，到 0x80000010。 这然后将它与**IHVBUS**组件 0x7FF，给出非零结果的筛选器掩码。 因此，第三个消息将传送到调试器中。

第四个消息传递给**DbgPrint**而不是**DbgPrintEx**。 在 Windows Server 2003 和 Windows 的早期版本中，消息传递到此例程始终传输。 在 Windows Vista 和更高版本的 Windows 中，消息传递到此例程总是会获得默认筛选器。 重要性位字段值等于 1 &lt; &lt; DPFLTR\_信息\_级别，即 0x00000008。 此例程的组件是**默认**。 由于你尚未设置**默认**组件筛选器掩码，它的值为 0x1。 此操作时它与重要性位字段，则结果为零。 因此不会传输的第四个消息。

### <a name="span-idthe-dbgprint-bufferspanspan-idthedbgprintbufferspanthe-dbgprint-buffer"></a><span id="the-dbgprint-buffer"></span><span id="THE_DBGPRINT_BUFFER"></span>DbgPrint 缓冲区

当**DbgPrint**， **DbgPrintEx**， **KdPrint**，或者**KdPrintEx**的消息传送到调试器，带格式的字符串发送到*DbgPrint 缓冲区*。 在大多数情况下，此缓冲区的内容是调试器命令窗口中立即显示。 可以通过使用来禁用此显示**缓冲区 DbgPrint 输出**的 Global Flags Utility (gflags.exe) 的选项。 此显示没有自动出现在本地内核调试过程。

在此显示已禁用的本地内核调试，和任何其他期间，DbgPrint 缓冲区的内容只能查看通过使用[ **！ dbgprint** ](-dbgprint.md)扩展命令。

调用的任何单个**DbgPrint**， **DbgPrintEx**， **KdPrint**，或者**KdPrintEx**仅传输 512 字节的信息。 超过这将会丢失任何输出。 DbgPrint 缓冲区本身可以免费版本的 Windows，保存最多 4 KB 的数据，并为 32 KB 的数据在签入生成的 Windows。 在 Windows Server 2003 和更高版本的 Windows 上，您可以使用 KDbgCtrl 工具更改 DbgPrint 缓冲区的大小。 请参阅[使用 KDbgCtrl](using-kdbgctrl.md)有关详细信息。

如果一条消息由于筛选出其*ComponentId*并*级别*值，通过调试连接不会传输。 因此，没有任何办法来在调试器中显示此消息。

 

 





