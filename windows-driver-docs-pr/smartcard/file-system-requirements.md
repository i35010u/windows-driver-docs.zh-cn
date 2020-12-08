---
title: 文件系统要求
description: 文件系统要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf26672609ea1a4f4137e99c30b31c24a7f6a32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811923"
---
# <a name="file-system-requirements"></a>文件系统要求


"逻辑" 布局是提供给基本 CSP/KSP 的数据布局。 此布局使用的是可读性更强的名称，并且这些文件可能不会与此卡采用的物理布局中的文件一一对应。

## <a name="span-idfile_naming_requirementsspanspan-idfile_naming_requirementsspanspan-idfile_naming_requirementsspanfile-naming-requirements"></a><span id="File_Naming_Requirements"></span><span id="file_naming_requirements"></span><span id="FILE_NAMING_REQUIREMENTS"></span>文件命名要求


文件名最多可包含八个 ANSI 字符 (8 位) ，不包括 Windows 文件和目录命名约定不允许的字符。 目录结构包括两个级别：应用程序使用的根目录和目录。 目录名称包含多达八个 ANSI 字符。 若要生成不区分大小写的文件名和目录名，卡微型驱动程序实现应将字符串转换为小写。

## <a name="span-idfile_naming_virtualizationspanspan-idfile_naming_virtualizationspanspan-idfile_naming_virtualizationspanfile-naming-virtualization"></a><span id="File_Naming_Virtualization"></span><span id="file_naming_virtualization"></span><span id="FILE_NAMING_VIRTUALIZATION"></span>文件命名虚拟化


允许实现卡微型驱动程序中的虚拟文件系统，将目录和文件映射到卡上的适当位置。 在正常操作期间不允许写入操作的卡 (如国家 ID 卡) 可以模拟写入操作，但必须在插入卡时保留 "写入" 的所有文件，并且在读取时必须能够返回这些文件。

## <a name="span-id_physical_card_data_layoutspanspan-id_physical_card_data_layoutspanspan-id_physical_card_data_layoutspan-physical-card-data-layout"></a><span id="_Physical_Card_Data_Layout"></span><span id="_physical_card_data_layout"></span><span id="_PHYSICAL_CARD_DATA_LAYOUT"></span> 物理卡数据布局


有关卡片上文件的以下信息概述了如何使用卡和文件系统。 不应将卡微型驱动程序设计为具有这些文件或其内容的知识。 应将卡微型驱动程序编写为通用接口层。

## <a name="span-idlogical_data_layoutspanspan-idlogical_data_layoutspanspan-idlogical_data_layoutspanlogical-data-layout"></a><span id="Logical_Data_Layout"></span><span id="logical_data_layout"></span><span id="LOGICAL_DATA_LAYOUT"></span>逻辑数据布局


### <a name="span-idcard_identifierspanspan-idcard_identifierspanspan-idcard_identifierspancard-identifier"></a><span id="Card_Identifier"></span><span id="card_identifier"></span><span id="CARD_IDENTIFIER"></span>卡标识符

卡标识符是卡的唯一标识符。 它可以在用户界面中以某种形式表示给用户，但在其他情况下，它仅用于与引用值进行比较以建立卡的标识。 为用户准备好卡时，将分配此值。 它被组织为一个字节数组。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>文件名  
此文件的逻辑名称为 "CardId"。 它在根目录中。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件为 E (R) 、U (R) 和 (RW) 。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>目录  
该文件被组织为16字节数组。 它应视为不透明的二进制数据。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
此值由 Microsoft 软件分配，以确保为卡生成唯一值。 它与在生产过程中可能会或不会分配给该卡的序列号无关。

### <a name="span-idapplication_directoryspanspan-idapplication_directoryspanspan-idapplication_directoryspanapplication-directory"></a><span id="Application_Directory"></span><span id="application_directory"></span><span id="APPLICATION_DIRECTORY"></span>应用程序目录

应用程序目录文件包含固定长度的应用程序名称条目的列表。 应用程序目录名称是包含所有应用程序文件的逻辑子目录的名称。 对于使用 CAPI2 的应用程序，该名称为 "mscp"，索引值为零。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称为 "cardapps"。 它在根目录中。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件为 E (R) 、U (RW) 和 (RW) 。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>目录  
该文件被组织为一系列记录，其中包含一个字节索引，后跟一个以零结尾的应用程序名称字符串 (ANSI) 。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
应用程序的实现要求应用程序名称映射到卡上的唯一目录，还需要映射到卡缓存文件中应用程序数据的唯一索引。 智能卡应用程序目录允许应用程序在缓存文件中查找其索引值，方法是在应用程序目录中查找其名称，并记下出现此情况的位置索引。 该文件包含一个8字节记录，其中包含应用程序名称，在结尾处填充零。 应用程序名称可使用全部8个字节，因此不要求结果字符串以零结尾。 因此，"已创建" 的卡片的文件内容如下8个字节：

``` syntax
{‘mscp’,0,0,0,0}
```

### <a name="span-idcache_filespanspan-idcache_filespanspan-idcache_filespancache-file"></a><span id="Cache_File"></span><span id="cache_file"></span><span id="CACHE_FILE"></span>缓存文件

为了提高性能并减少与卡的通信，基本 CSP/KSP 可以通过多种方式缓存卡数据。 缓存文件用于通过指示卡上数据的版本号来控制基本 CSP/KSP 中缓存子系统的操作。 更改数据时，此值会递增。 将缓存文件的内部副本与从卡读取的版本进行比较，使基本 CSP/KSP 能够确定是否可以使用或刷新缓存的数据。 做出这种决定的需要有多种原因，包括取出和重新插入卡。

从卡读取卡标识符和缓存文件应该完全足以允许使用缓存在主机上不确定的时间段的信息。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称为 "CardCF"。 它在根目录中。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件为 E (R) 、U (RW) 和 (RW) 。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>目录  
该文件是以2个字节值的形式组织的全局数据，后跟应用程序维护和解释的32位缓存值连续。 其中的第一个保留用于要使用的基本 CSP/KSP。 此后，将为每个应用程序分配一个 **DWORD**。

``` syntax
typedef struct _CARD_CACHE_FILE_FORMAT
{
    BYTE bVersion;          // Cache version
    BYTE bPinsFreshness;        // Card PIN
    WORD wContainersFreshness;
    WORD wFilesFreshness;

} CARD_CACHE_FILE_FORMAT, *PCARD_CACHE_FILE_FORMAT;
```

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
如果应用程序内部的缓存数据复制对所需数据的版本号不同于从卡片读取的文件，则会刷新应用程序的内部缓存。 通常，在每个事务开始时，将在卡上检查缓存。

应用程序缓存数据 Dword 数组（每个缓存应用程序一个）由应用程序目录文件中的应用程序索引进行索引。 添加应用程序时，文件将以4字节的增量增长。

### <a name="span-idcontainer_map_filespanspan-idcontainer_map_filespanspan-idcontainer_map_filespancontainer-map-file"></a><span id="Container_Map_File"></span><span id="container_map_file"></span><span id="CONTAINER_MAP_FILE"></span>容器映射文件

容器映射文件由基本 CSP/KSP 拥有，由多个 CONTAINERMAPRECORD 类型的记录组成。 这些记录将容器标识符（通常是由 CAPI 分配的 GUID）与可用于访问该容器的密钥和证书的索引相关联。

文件中记录 (索引) 位置对应于与该容器关联的证书和密钥信息的索引。 因此，此类文件中的第二条记录将显示从零开始的索引1。

与此容器关联的证书以及该容器的签名和/或密钥交换密钥都共享此索引 (UserCerts \\ SignatureCert1、SignatureKey1 等) 。 记录包含与该索引关联的密钥的容器 GUID 和大小信息。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称为 "CMapFile"。 它位于 "mscp" 目录中。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件为 E (R) 、U (RW) 和 (RW) 。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>目录  
此文件的访问条件为 E (R) 、U (RW) 和 (RW) 。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
此文件由基本 CSP/KSP 维护并维护其内容。 仅提供有关此文件内部结构的信息以供参考。 文件中的记录采用以下格式：

**CONTAINERMAPRECORD**

这些记录包含 CAPI 分配的容器 GUID，以及与该容器关联的关联密钥交换或签名密钥的密钥大小。 所有 WORD 成员都是 Endean 字节顺序。

``` syntax
//
// Type: CONTAINER_MAP_RECORD
//
// This structure describes the format of the Base CSP's 
// container map file, stored on the card. This is well-known 
// logical file wszCONTAINER_MAP_FILE. The file consists of 
// zero or more of these records.
//
#define MAX_CONTAINER_NAME_LEN                  39

// This flag is set in the CONTAINER_MAP_RECORD bFlags 
// member if the corresponding container is valid and currently 
// exists on the card. // If the container is deleted, its 
// bFlags field must be cleared.
#define CONTAINER_MAP_VALID_CONTAINER           1

// This flag is set in the CONTAINER_MAP_RECORD bFlags
// member if the corresponding container is the default
// container on the card.
define CONTAINER_MAP_DEFAULT_CONTAINER         2

typedef struct _CONTAINER_MAP_RECORD
{
    WCHAR wszGuid [MAX_CONTAINER_NAME_LEN + 1];
    BYTE bFlags;
    BYTE bReserved;
    WORD wSigKeySizeBits;
    WORD wKeyExchangeKeySizeBits;
} CONTAINER_MAP_RECORD, *PCONTAINER_MAP_RECORD;
```

**WszGuid** 成员包含 CAPI 分配给容器的标识符的 UNICODE 字符串表示形式。 这通常（但不总是） GUID 字符串。 标识符名称不能包含特殊字符 " \\ "。 预配只读卡后，预配过程必须遵循相同的标识符名称准则。

容器名称必须以 null 结尾，且不得大于 (最大 \_ 容器名称长度 \_ 为 \_ + 1) 个字符，包括 null 终止符。

如果必须从此表中删除记录，则会通过将零写入记录来使条目失效。 以后可以使用新数据覆盖此类记录。 该表未 "打包" 以删除不活动的条目。

以下位适用于 Flags 字节：

-   如果容器记录有效，则设置位0。
-   当容器为默认值时，设置第1位。 仅容器映射中的一条记录可以随时设置此位。 只有在设置了位0的情况下，才可以设置此位。 换句话说，不能有无效的默认容器。 所有其他位当前保留，以供将来版本的卡微型驱动程序。
-   对于默认容器，这将转换为字节的0x03。 对于默认情况下的有效容器，此值为0x01。
-   Bits 2-7 保留供将来使用。

## <a name="span-iddata_layout_summaryspanspan-iddata_layout_summaryspanspan-iddata_layout_summaryspandata-layout-summary"></a><span id="Data_Layout_Summary"></span><span id="data_layout_summary"></span><span id="DATA_LAYOUT_SUMMARY"></span>数据布局摘要


下表总结了卡微型驱动程序与用于典型实现的基本 CSP/KSP 之间的接口上的数据组织。 "逻辑名称" 是基本 CSP/KSP 用于与卡微型驱动程序通信的字符串;它可能会也可能不会直接映射到卡片上的对应元素。

请注意，证书和密钥根据其用途以逻辑方式分组到子目录，只是使用实际文件名的索引。 添加到卡中的任何证书或密钥都根据它们在目录中的索引号进行命名。 下表显示了一些示例证书和密钥，以便进行说明。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目录名称</th>
<th align="left">文件名</th>
<th align="left">类型</th>
<th align="left">访问条件</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardid</td>
<td align="left">文件</td>
<td align="left">E (R) U (R)  (RW) </td>
<td align="left">卡标识符</td>
</tr>
<tr class="even">
<td align="left">&lt;root&gt;</td>
<td align="left">cardcf</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left">缓存文件</td>
</tr>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardapps</td>
<td align="left">文件</td>
<td align="left">E (R) U (R)  (RW) </td>
<td align="left"><p>按应用程序名称的目录索引。</p>
<p>有关详细信息，请参阅 "应用程序目录"。</p></td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left"></td>
<td align="left">Dir</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left">基本 CSP/KSP 应用目录</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">cmapfile</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left">要编制索引的 CAPI GUID</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">kxc00</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left"> (示例) 密钥交换证书0</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">ksc00</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left"> (示例) 密钥签名证书0</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">ksc01</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left"> (示例) 密钥签名证书1</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">msroots</td>
<td align="left">文件</td>
<td align="left">E (R) U (RW)  (RW) </td>
<td align="left">企业受信任的根</td>
</tr>
</tbody>
</table>

 

**注意**  与 msroots： mscp \\ msroots 文件的互操作性是 PKCS \# 7 格式的证书存储区。

 

## <a name="span-idfile_access_controlspanspan-idfile_access_controlspanspan-idfile_access_controlspanfile-access-control"></a><span id="File_Access_Control"></span><span id="file_access_control"></span><span id="FILE_ACCESS_CONTROL"></span>文件访问控制


### <a name="span-idknown_principalsspanspan-idknown_principalsspanspan-idknown_principalsspanknown-principals"></a><span id="Known_Principals"></span><span id="known_principals"></span><span id="KNOWN_PRINCIPALS"></span>已知主体

已知主体是各种类型的用户的标识符，可尝试以某种方式访问卡数据。 下表显示了有效的主体，其中包含一个字母缩写，可与数据访问操作标识符一起用于定义访问条件。 尽管可能存在更多可识别主体，但列表限制为对基本 CSP/KSP 和卡微型驱动程序之间的通信有意义的。

| “属性”          | 描述                                                                                                                                                                                                                                                                                 | 助记符 | PIN \_ ID 映射    |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|--------------------|
| 所有人      | 任何请求者，包括未经身份验证的 (或匿名) 用户。                                                                                                                                                                                                                              | E        | 角色 \_ 每个人 (0)  |
| User          | 智能卡的用户客户端，通过使用 PIN 向卡证明其身份。                                                                                                                                                                                                             | U        | 角色 \_ 用户 (1)      |
| 管理员 | 卡颁发者或与卡上的数据具有管理关系的其他参与方。 使用特定的 PIN 或密钥 (，这些密钥或可能对卡或用户不唯一) 执行用户无法执行的管理任务，而无需使用此类数据，如 PIN 取消阻止。 | A        | 角色 \_ 管理员 (2)     |

 

在以下讨论中使用 "每个人" 时，它通常表示智能卡的任何用户（无论是否经过身份验证）。 例如，"所有人都可以读取文件"，这意味着用户或管理员可以自动读取文件。

对于文件系统访问权限，管理员通常被视为 "超级用户"，并具有与用户 (相同的权限，) 执行特权除外。

### <a name="span-iddirectory_access_conditionsspanspan-iddirectory_access_conditionsspanspan-iddirectory_access_conditionsspandirectory-access-conditions"></a><span id="Directory_Access_Conditions"></span><span id="directory_access_conditions"></span><span id="DIRECTORY_ACCESS_CONDITIONS"></span>目录访问条件

主体可以在包含两组权限的卡文件系统中创建目录。 下表总结了每个权限的影响。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目录访问条件</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">UserCreateDeleteDirAc</td>
<td align="left"><p>用户和管理员可以使用 <a href="/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](/previous-versions/dn468711(v=vs.85))"><strong>CardCreateFile</strong></a>在目录中创建文件。</p>
<p>用户和管理员可以通过调用 <a href="/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](/previous-versions/dn468716(v=vs.85))"><strong>CardDeleteDirectory</strong></a>来删除不为空) 目录 (。</p>
<p>所有人都可以使用 <a href="/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](/previous-versions/dn468721(v=vs.85))"><strong>CardEnumFiles</strong></a>列出目录的内容。</p></td>
</tr>
<tr class="even">
<td align="left">AdminCreateDeleteDirAc</td>
<td align="left"><p>管理员可以使用 <a href="/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](/previous-versions/dn468711(v=vs.85))"><strong>CardCreateFile</strong></a>在目录中创建文件。</p>
<p>管理员可以使用 <a href="/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](/previous-versions/dn468716(v=vs.85))"><strong>CardDeleteDirectory</strong></a>删除该目录。</p>
<p>所有人都可以使用 <a href="/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](/previous-versions/dn468721(v=vs.85))"><strong>CardEnumFiles</strong></a>列出目录的内容。</p>
<div class="alert">
<strong>注意</strong>  此 ACL 是可选的。 它可能会从智能卡微型驱动程序规范的将来版本中删除。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**注意**  创建目录时，每个人都有权列出目录中的文件。 目录没有单独的 "列表" 权限。

 

### <a name="span-idfile_access_operationsspanspan-idfile_access_operationsspanspan-idfile_access_operationsspanfile-access-operations"></a><span id="File_Access_Operations"></span><span id="file_access_operations"></span><span id="FILE_ACCESS_OPERATIONS"></span>文件访问操作

主体可以通过多种方式使用文件的内容。 下表列出了有效的操作，其中包含一个字母缩写，可用于定义访问条件。 特别要注意的是，执行 (X) 与其他文件访问操作没有逻辑关系，这是一项独立操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作/特权</th>
<th align="left">描述</th>
<th align="left">助记符</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">读取</td>
<td align="left"><p>直接或以格式化或处理型形式接收文件的内容。</p></td>
<td align="left">R</td>
</tr>
<tr class="even">
<td align="left">写入</td>
<td align="left"><p>更改文件的内容，可能会创建文件，或者删除、替换或更改现有数据。</p></td>
<td align="left">W</td>
</tr>
<tr class="odd">
<td align="left">执行</td>
<td align="left"><p>使用文件内容执行请求程序中由卡执行的操作，而不能接收数据以便使用或册派生。</p></td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

### <a name="span-id_file_access_conditionsspanspan-id_file_access_conditionsspanspan-id_file_access_conditionsspan-file-access-conditions"></a><span id="_File_Access_Conditions"></span><span id="_file_access_conditions"></span><span id="_FILE_ACCESS_CONDITIONS"></span> 文件访问条件

访问条件与 Acl 类似。 访问条件控制哪些主体可以访问给定文件以及它们可以执行哪些操作。 卡片上的每个文件都有一个访问条件，可以通过主体列表及其访问权限来进行描述。 如果描述中不包含主体或特权，则假定其被拒绝。 一般而言，对卡执行访问条件。

下表列出了通过 [**CardCreateFile**](/previous-versions/dn468711(v=vs.85)) 可用的访问条件，并将它们映射到适当的访问条件助记键。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文件访问条件</th>
<th align="left">实际含义</th>
<th align="left">访问条件助记键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">InvalidAc</td>
<td align="left"><p>检索 ACL 时出错。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">EveryoneReadUserWriteAc</td>
<td align="left"><p>这意味着，每个人都可以分别读取文件或获取 (<a href="/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](/previous-versions/dn468727(v=vs.85))"><strong>CardReadFile</strong></a> 或 <strong>CardGetFileInfo</strong>) 的文件信息，并且用户和管理员可以读取文件、写入文件以及删除文件。</p></td>
<td align="left">E (R) ，U (RW) ， (RW) </td>
</tr>
<tr class="odd">
<td align="left">UserWriteExecuteAc</td>
<td align="left"><p>用户可以编写文件，可以 "执行" 文件，并可以删除文件。 不包括用户在内的任何人都可以读取文件的内容。 管理员还可以写入但不能执行此文件的内容，并可以删除该文件。</p></td>
<td align="left">U (WX)  (W) </td>
</tr>
<tr class="even">
<td align="left">EveryoneReadAdminWriteAc</td>
<td align="left"><p>这意味着，每个人都可以分别读取文件或获取 (<a href="/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](/previous-versions/dn468727(v=vs.85))"><strong>CardReadFile</strong></a> 或 <strong>CardGetFileInfo</strong>) 的文件信息，但只有管理员才能写入文件和删除文件。</p></td>
<td align="left">E (R) ，U (R) ， (RW) </td>
</tr>
<tr class="odd">
<td align="left">UnknownAc</td>
<td align="left"><p>此文件由不属于预定义 AC 类型的卡上 (AC) 的访问条件所保护。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">UserReadWriteAc</td>
<td align="left"><p>所有人都不能访问//用户读写////////////////</p></td>
<td align="left">U (RW) ， (RW) </td>
</tr>
<tr class="odd">
<td align="left">AdminReadWriteAc</td>
<td align="left"><p>每个人/用户无访问权限</p>
<p>管理员读取写入</p>
<p>//</p>
<p>示例：管理数据。</p></td>
<td align="left"> (RW) </td>
</tr>
</tbody>
</table>

 

下表列出了常见项的一些示例访问条件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">访问条件</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">E (X) U (W)  () </td>
<td align="left"><p>这是用户 PIN 的访问条件。 当需要 PIN 的操作开始时，用户未被识别。 必须 "执行" PIN 才能建立用户的标识。 输入 PIN 后，用户的标识将从 E 升级到 U。用户和管理员都可以写入 PIN。</p></td>
</tr>
<tr class="even">
<td align="left">U (WX)  (W) </td>
<td align="left"><p>用户的私钥文件永远不能从卡读取，并且只有用户可以使用其内容来执行加密操作。 用户或管理员可以更改此数据。</p></td>
</tr>
<tr class="odd">
<td align="left">E (R) U (R)  (RW) </td>
<td align="left"><p>卡标识符。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idnotes_on_the_directory_and_file_access_conditionsspanspan-idnotes_on_the_directory_and_file_access_conditionsspanspan-idnotes_on_the_directory_and_file_access_conditionsspannotes-on-the-directory-and-file-access-conditions"></a><span id="Notes_on_the_Directory_and_File_Access_Conditions"></span><span id="notes_on_the_directory_and_file_access_conditions"></span><span id="NOTES_ON_THE_DIRECTORY_AND_FILE_ACCESS_CONDITIONS"></span>有关目录和文件访问条件的说明

-   主体需要对文件的读取访问权限， [**CardGetFileInfo**](/previous-versions/dn468727(v=vs.85)) 才能成功。
-   没有单独的列表权限列出目录的内容。
-   "创建对目录的访问权限" 意味着具有在目录中创建文件的权限，而 "删除对目录的访问权限" 意味着具有删除目录本身的权限。 若要删除文件，卡主体必须对文件本身具有写入访问权限。
-   不能通过智能卡微型驱动程序接口创建具有 E (W) 权限的目录。
-   不能通过智能卡微型驱动程序接口更改文件或目录权限，而无需删除并重新创建文件或目录。
-   不能通过智能卡微型驱动程序接口创建由管理员或未通过身份验证的用户拥有的私钥文件。
-   不可能通过智能卡微型驱动程序接口在卡上创建 PIN 文件 (E (X) 、U (W) 和 (W) # A7。
-   不可能通过智能卡微型驱动程序接口来查询目录访问条件。
-   只有通过智能卡微型驱动程序接口才能使用可用的访问条件组合的子集创建文件。

