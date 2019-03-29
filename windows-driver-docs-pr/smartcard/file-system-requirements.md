---
title: 文件系统要求
description: 文件系统要求
ms.assetid: 2C363978-3C98-4838-8C55-F804D2C75BEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec3acad4a88463a2cc1c85cd2cd7f84a41579e1
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349646"
---
# <a name="file-system-requirements"></a>文件系统要求


"逻辑"布局是提供对基本 CSP/KSP 的数据布局。 此布局使用更多的用户可读名称，并将文件可能不对应一对一卡使用的物理布局中的文件。

## <a name="span-idfilenamingrequirementsspanspan-idfilenamingrequirementsspanspan-idfilenamingrequirementsspanfile-naming-requirements"></a><span id="File_Naming_Requirements"></span><span id="file_naming_requirements"></span><span id="FILE_NAMING_REQUIREMENTS"></span>文件命名要求


文件的名称由最多八个 ANSI 字符 （8 位），不包括 Windows 文件和目录命名约定不允许的字符组成。 目录结构包含两个级别： 根目录和应用程序使用的目录。 目录名称由最多八个 ANSI 字符组成。 若要生成的文件名和目录名的不区分大小写，卡微型驱动程序实现应将字符串转换为小写。

## <a name="span-idfilenamingvirtualizationspanspan-idfilenamingvirtualizationspanspan-idfilenamingvirtualizationspanfile-naming-virtualization"></a><span id="File_Naming_Virtualization"></span><span id="file_naming_virtualization"></span><span id="FILE_NAMING_VIRTUALIZATION"></span>文件命名的虚拟化


它是允许在将目录和文件映射到在卡上的适当位置卡微型驱动程序中实现虚拟文件系统。 不允许的卡写入操作 （如国家/地区 ID 卡） 的正常操作期间可能会模拟的写入操作，但必须维护任何文件的"编写"卡的插入操作的持续时间内，并且必须能够以返回这些文件时它们为只读。

## <a name="span-idphysicalcarddatalayoutspanspan-idphysicalcarddatalayoutspanspan-idphysicalcarddatalayoutspan-physical-card-data-layout"></a><span id="_Physical_Card_Data_Layout"></span><span id="_physical_card_data_layout"></span><span id="_PHYSICAL_CARD_DATA_LAYOUT"></span> 物理卡数据布局


有关在卡上的文件的以下信息是如何使用卡和文件系统的概述。 它不是，应了解这些文件或其内容与设计卡微型驱动程序。 卡微型驱动程序应编写为一个通用的接口层。

## <a name="span-idlogicaldatalayoutspanspan-idlogicaldatalayoutspanspan-idlogicaldatalayoutspanlogical-data-layout"></a><span id="Logical_Data_Layout"></span><span id="logical_data_layout"></span><span id="LOGICAL_DATA_LAYOUT"></span>逻辑数据布局


### <a name="span-idcardidentifierspanspan-idcardidentifierspanspan-idcardidentifierspancard-identifier"></a><span id="Card_Identifier"></span><span id="card_identifier"></span><span id="CARD_IDENTIFIER"></span>卡标识符

卡标识符是卡片的唯一标识符。 它可能会以某种形式呈现给用户在 UI 中，但否则仅用于与引用值之间的比较来建立一个卡的标识。 此值分配为用户准备在卡时。 它被组织为一个字节数组。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>文件的名称  
此文件的逻辑名称是"CardId"。 它是在根目录下。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件是 E(R)、 U(R) 和 A(RW)。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
文件组织为一个 16 字节数组。 它应视为不透明二进制数据。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
此值是由分配 Microsoft 软件以确保为卡生成唯一值。 很可能会或可能不分配到卡在制造过程的序列号不相关。

### <a name="span-idapplicationdirectoryspanspan-idapplicationdirectoryspanspan-idapplicationdirectoryspanapplication-directory"></a><span id="Application_Directory"></span><span id="application_directory"></span><span id="APPLICATION_DIRECTORY"></span>应用程序目录

应用程序目录文件包含固定长度的应用程序名称项的列表。 应用程序目录名称是包含的所有应用程序的文件的逻辑子目录的名称。 对于使用 CAPI2 的应用程序，名称是"mscp"的索引值为零。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称是"cardapps"。 它是在根目录下。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件是 E(R)、 U(RW) 和 A(RW)。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
文件组织为一系列记录，其中包含零终止应用程序名称字符串 (ANSI) 后跟的字节索引。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
应用程序的实现要求应用程序名称映射到在卡上的唯一目录和应用程序的数据卡缓存文件中的唯一索引。 卡应用程序目录允许应用程序在缓存文件中查找其索引值，通过在应用程序目录中查找其名称并记下这种情况发生的位置的索引。 8 个字节记录，其中包含应用程序名称，该文件由零填充结束时。 应用程序名称可以使用所有 8 个字节，以便生成的字符串以零结尾没有要求。 因此，"创建"卡文件的内容是以下 8 个字节：

``` syntax
{‘mscp’,0,0,0,0}
```

### <a name="span-idcachefilespanspan-idcachefilespanspan-idcachefilespancache-file"></a><span id="Cache_File"></span><span id="cache_file"></span><span id="CACHE_FILE"></span>缓存文件

若要提高性能并减少与卡一起通信，基本 CSP/KSP 可以缓存以各种方式的卡数据。 缓存文件用于通过，该值指示数据在卡上的版本号来控制缓存的子系统中基本 CSP/KSP 的操作。 数据更改时，此值都会递增。 基本 CSP/KSP 以确定是否可以使用缓存的数据，或者必须刷新，比较其内部与已从卡中读取的版本的缓存文件的副本。 原因有多种，包括要撤消和重新插入卡可能需要做出此判断。

读取从智能卡的卡标识符和缓存文件应完全不足以允许使用缓存的主机上的时间不确定时间的信息。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称是"CardCF"。 它是在根目录下。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件是 E(R)、 U(RW) 和 A(RW)。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
该文件是组织的全局数据形式的 2 字节值后跟一系列应用程序维护和解释的 32 位缓存值。 其中第一个保留用于基本 CSP/KSP 使用。 此后，每个应用程序分配一个**DWORD**。

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
如果是内部应用程序的缓存数据副本指示不同的版本号的数据比从卡中读取文件所需的，刷新应用程序的内部缓存。 与卡一起缓存通常检查每个事务的开始处。

为应用程序提供缓存数据 dword 值，一个用于每个缓存的应用程序，数组是通过从应用程序目录文件中的应用程序索引编制索引。 添加应用程序时，则文件将增长的 4 字节为增量。

### <a name="span-idcontainermapfilespanspan-idcontainermapfilespanspan-idcontainermapfilespancontainer-map-file"></a><span id="Container_Map_File"></span><span id="container_map_file"></span><span id="CONTAINER_MAP_FILE"></span>容器映射文件

容器映射文件拥有通过基本 CSP/KSP，包含的 CONTAINERMAPRECORD 类型的记录数。 这些记录将关联的容器标识符，这通常是一个 GUID，被 CAPI 赋予的索引，可用于访问密钥和容器的证书。

（索引） 的记录的文件中的位置对应的证书和与该容器关联的密钥信息的索引。 因此，此类文件中的第二个记录将看到从零开始索引为 1。

与此容器和所有容器的签名和/或密钥交换密钥相关联的证书共享此索引 (UserCerts\\SignatureCert1、 SignatureKey1，等等)。 记录包含容器 GUID 和与该索引关联的密钥的大小信息。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>逻辑名称  
此文件的逻辑名称是"CMapFile"。 它是"mscp"目录中。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>访问条件  
此文件的访问条件是 E(R)、 U(RW) 和 A(RW)。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
此文件的访问条件是 E(R)、 U(RW) 和 A(RW)。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注  
创建此文件和其内容维护的基本 CSP/KSP。 仅适用于参考提供了有关此文件的内部结构的信息。 在文件中的记录具有以下格式：

**CONTAINERMAPRECORD**

这些记录包含 CAPI 分配容器 GUID 和关联的密钥交换或签名与该容器关联的密钥的密钥大小。 所有 WORD 成员都是小 Endean 字节顺序。

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

**WszGuid**成员包含的 UNICODE 字符的字符串表示形式 CAPI 赋给容器的标识符。 这是通常情况下，但并不总是一个 GUID 字符串。 标识符名称不能包含特殊字符"\\"。 只读卡设置时，预配过程必须遵循标识符名称的相同准则。

容器名称必须以 null 结尾并且不能晚于 (最大\_容器\_名称\_LEN + 1) 中包括 NULL 终止符的长度的字符。

如果必须从该表中删除一条记录，该条目会通过编写与记录零失效。 此类记录更高版本的新数据会被覆盖。 表不"打包"以删除不活动的条目。

以下位标志字节的有效值：

-   容器记录有效时，位 0 设置。
-   当容器为默认设置位 1。 容器映射中的只有一条记录可以在任何时候设置位。 仅当还设置位 0，则可以设置此位。 换而言之，不能具有不是有效的默认容器。 卡微型驱动程序的未来版本的当前保留的所有其他位。
-   对于默认容器中，这会转换为字节 0x03。 对于不是默认值是有效的容器，此值为 0x01。
-   2-7 位被保留供将来使用。

## <a name="span-iddatalayoutsummaryspanspan-iddatalayoutsummaryspanspan-iddatalayoutsummaryspandata-layout-summary"></a><span id="Data_Layout_Summary"></span><span id="data_layout_summary"></span><span id="DATA_LAYOUT_SUMMARY"></span>数据布局摘要


下表总结了卡微型驱动程序与基本 CSP/KSP 的一个典型的实现之间的接口上的数据的组织。 "逻辑 Name"是基本 CSP/KSP 使用卡微型驱动程序; 与进行通信的字符串它可能会或可能不能直接映射到在卡上的相应元素。

请注意，证书和密钥以逻辑方式分组的基本 CSP/KSP 到子目录按其目的仅索引使用的实际文件名称。 根据其在其目录中的索引号命名任何证书或密钥添加到卡。 出于演示目的下表中显示某些示例证书和密钥。

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
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">访问条件</th>
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardid</td>
<td align="left">文件</td>
<td align="left">E(R) U(R) A(RW)</td>
<td align="left">卡标识符</td>
</tr>
<tr class="even">
<td align="left">&lt;root&gt;</td>
<td align="left">cardcf</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">缓存文件</td>
</tr>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardapps</td>
<td align="left">文件</td>
<td align="left">E(R) U(R) A(RW)</td>
<td align="left"><p>按应用程序名称的目录索引。</p>
<p>有关详细信息，请参阅应用程序目录。</p></td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left"></td>
<td align="left">dir</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">基本 CSP/KSP 应用目录</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">cmapfile</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">CAPI GUID 传递给索引</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">kxc00</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">（示例） 密钥交换证书 0</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">ksc00</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">（示例） 密钥签名证书 0</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">ksc01</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">（示例） 密钥签名证书 1</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">msroots</td>
<td align="left">文件</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">包括受信任企业根</td>
</tr>
</tbody>
</table>

 

**请注意**  msroots 与互操作性： mscp\\msroots 文件是 PKCS \#7 格式的证书存储区。

 

## <a name="span-idfileaccesscontrolspanspan-idfileaccesscontrolspanspan-idfileaccesscontrolspanfile-access-control"></a><span id="File_Access_Control"></span><span id="file_access_control"></span><span id="FILE_ACCESS_CONTROL"></span>文件访问控制


### <a name="span-idknownprincipalsspanspan-idknownprincipalsspanspan-idknownprincipalsspanknown-principals"></a><span id="Known_Principals"></span><span id="known_principals"></span><span id="KNOWN_PRINCIPALS"></span>已知的主体

已知的主体是可以尝试访问以某种方式的卡数据的用户的各种类型的标识符。 下表显示了有效的主体，可以与数据访问操作标识符一起使用来定义访问条件的单个字母缩写。 尽管可以有多个身份主体，但列的部分是限制为那些对基本 CSP/KSP 和卡微型驱动程序之间的通信有含义。

| 名称          | 描述                                                                                                                                                                                                                                                                                 | 助记键 | PIN\_ID 映射    |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|--------------------|
| Everyone      | 任何请求者，包括未经身份验证 （或匿名） 的用户。                                                                                                                                                                                                                              | E        | 角色\_EVERYONE (0) |
| “用户”          | 用户客户端的卡，用户通过使用 PIN 到卡证明其身份。                                                                                                                                                                                                             | U        | 角色\_用户 (1)     |
| 管理员 | 信用卡颁发机构或另一方具有对卡或卡上的数据管理关系。 使用特殊的 PIN 或键 （即可能或可能不是唯一的卡或用户） 来执行，而无需使用此数据，如 PIN 解除阻止用户无法执行的管理任务。 | A        | 角色\_管理员 (2)    |

 

在下面的讨论中使用"everyone"时，则通常意味着在卡中，任何用户是否经过身份验证或不。 例如，"每个人都可以读取文件，"意味着用户或管理员可以自动读取该文件。

对文件系统访问，管理员通常都被视为"超级用户"，并作为 （除了 execute 权限） 用户具有完全相同的权限。

### <a name="span-iddirectoryaccessconditionsspanspan-iddirectoryaccessconditionsspanspan-iddirectoryaccessconditionsspandirectory-access-conditions"></a><span id="Directory_Access_Conditions"></span><span id="directory_access_conditions"></span><span id="DIRECTORY_ACCESS_CONDITIONS"></span>目录访问条件

主体可以使用两组权限卡文件系统中创建目录。 下表总结了每个权限的影响。

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
<td align="left"><p>用户和管理员可以创建文件的目录中通过使用<a href="https://msdn.microsoft.com/library/windows/hardware/dn468711" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468711)"> <strong>CardCreateFile</strong></a>。</p>
<p>用户和管理员可以删除的目录 （如果不为空），通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/dn468716" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468716)"> <strong>CardDeleteDirectory</strong></a>。</p>
<p>每个人都可以通过使用列出目录的内容<a href="https://msdn.microsoft.com/library/windows/hardware/dn468721" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468721)"> <strong>CardEnumFiles</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left">AdminCreateDeleteDirAc</td>
<td align="left"><p>管理员可以创建文件的目录中通过使用<a href="https://msdn.microsoft.com/library/windows/hardware/dn468711" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468711)"> <strong>CardCreateFile</strong></a>。</p>
<p>管理员可以通过删除目录<a href="https://msdn.microsoft.com/library/windows/hardware/dn468716" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468716)"> <strong>CardDeleteDirectory</strong></a>。</p>
<p>每个人都可以通过使用列出目录的内容<a href="https://msdn.microsoft.com/library/windows/hardware/dn468721" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468721)"> <strong>CardEnumFiles</strong></a>。</p>
<div class="alert">
<strong>请注意</strong>  此 ACL 是可选的。 它可能会从智能卡微型驱动程序规范的未来版本中删除。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**请注意**  时创建目录时，每个人都自动有权列出目录中的文件。 没有单独的"列表"权限的目录。

 

### <a name="span-idfileaccessoperationsspanspan-idfileaccessoperationsspanspan-idfileaccessoperationsspanfile-access-operations"></a><span id="File_Access_Operations"></span><span id="file_access_operations"></span><span id="FILE_ACCESS_OPERATIONS"></span>文件访问操作

主体可以使用各种方法中的文件的内容。 下表中，使用的单个字母缩写，可以使用，以及主体的指示符，来定义访问条件中列出有效的操作。 具体而言，请注意执行 (X)，有其他文件访问操作没有逻辑关系 — 它是独立的操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Operations/privileges</th>
<th align="left">描述</th>
<th align="left">助记键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Read</td>
<td align="left"><p>接收文件的内容直接或格式，或者处理窗体中。</p></td>
<td align="left">R</td>
</tr>
<tr class="even">
<td align="left">写入</td>
<td align="left"><p>更改文件，可能导致创建该文件，或删除、 替换或更改现有数据的内容。</p></td>
<td align="left">W</td>
</tr>
<tr class="odd">
<td align="left">执行</td>
<td align="left"><p>通过请求者的代表，卡而不需要能够接收因此所使用的数据执行的操作中使用文件内容或一点派生。</p></td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

### <a name="span-idfileaccessconditionsspanspan-idfileaccessconditionsspanspan-idfileaccessconditionsspan-file-access-conditions"></a><span id="_File_Access_Conditions"></span><span id="_file_access_conditions"></span><span id="_FILE_ACCESS_CONDITIONS"></span> 文件访问条件

访问条件是类似于 Acl。 访问的主体可以访问给定的文件和内容的条件控制他们可以执行的操作。 在卡上的每个文件具有访问条件，可以通过主体和其访问权限的列表所述。 如果某一主体或特权未包含在说明中，则假定要对其拒绝。 通常情况下，在卡上强制实施访问条件。

下表列出了可通过访问条件[ **CardCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/dn468711)并将它们映射到适当的访问条件助记键。

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
<td align="left"><p>这意味着每个人都可以读取该文件或获取文件信息 (<a href="https://msdn.microsoft.com/library/windows/hardware/dn468727" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468727)"><strong>CardReadFile</strong> </a>或<strong>CardGetFileInfo</strong>) 分别，并且用户和管理员可以读取文件，写入该文件，并删除该文件。</p></td>
<td align="left">E(R)，U(RW)，A(RW)</td>
</tr>
<tr class="odd">
<td align="left">UserWriteExecuteAc</td>
<td align="left"><p>用户可以写入该文件，可以"执行"文件，并可以删除该文件。 任何人，包括用户，可以读取该文件的内容。 管理员可以还编写，但不是执行内容的此文件，可以删除该文件。</p></td>
<td align="left">U(WX) A(W)</td>
</tr>
<tr class="even">
<td align="left">EveryoneReadAdminWriteAc</td>
<td align="left"><p>这意味着每个人都可以读取该文件或获取文件信息 (<a href="https://msdn.microsoft.com/library/windows/hardware/dn468727" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468727)"><strong>CardReadFile</strong> </a>或<strong>CardGetFileInfo</strong>) 分别，但是，只有管理员可以编写文件和删除文件。</p></td>
<td align="left">E(R)，U(R)，A(RW)</td>
</tr>
<tr class="odd">
<td align="left">UnknownAc</td>
<td align="left"><p>该文件受访问条件 (AC) 不是预定义的 AC 类型之一在卡上。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">UserReadWriteAc</td>
<td align="left"><p>每个人都没有访问权限 / 用户读写 / / / / 示例：密码钱包文件</p></td>
<td align="left">U(RW), A(RW)</td>
</tr>
<tr class="odd">
<td align="left">AdminReadWriteAc</td>
<td align="left"><p>所有人 / 用户没有访问权限</p>
<p>管理员读写</p>
<p>//</p>
<p>示例：管理数据。</p></td>
<td align="left">A(RW)</td>
</tr>
</tbody>
</table>

 

下表列出了一些示例访问条件的常见项。

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
<td align="left">E(X) U(W) A(W)</td>
<td align="left"><p>这将是访问条件的用户 PIN。 需要 PIN 的操作开始时，用户是无法识别。 PIN 必须在"执行"以建立用户的标识。 PIN 的项之后, 用户的标识将提升从电子为 u。用户和管理员可以编写一个 PIN。</p></td>
</tr>
<tr class="even">
<td align="left">U(WX) A(W)</td>
<td align="left"><p>可能永远不会从卡中读取用户的私钥文件，仅用户可为加密操作使用其内容。 此数据可能会由用户或管理员更改。</p></td>
</tr>
<tr class="odd">
<td align="left">E(R) U(R) A(RW)</td>
<td align="left"><p>卡标识符。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idnotesonthedirectoryandfileaccessconditionsspanspan-idnotesonthedirectoryandfileaccessconditionsspanspan-idnotesonthedirectoryandfileaccessconditionsspannotes-on-the-directory-and-file-access-conditions"></a><span id="Notes_on_the_Directory_and_File_Access_Conditions"></span><span id="notes_on_the_directory_and_file_access_conditions"></span><span id="NOTES_ON_THE_DIRECTORY_AND_FILE_ACCESS_CONDITIONS"></span>有关目录和文件访问条件的说明

-   主体需要的文件的读取访问权限[ **CardGetFileInfo** ](https://msdn.microsoft.com/library/windows/hardware/dn468727)才能成功。
-   没有单独的列表的权限以列出目录的内容。
-   "创建对目录访问"意味着您在目录中，创建文件的权限而"删除的目录的访问权限"，这意味着删除目录本身的权限。 若要删除的文件，主体卡必须到该文件本身具有写访问权限。
-   不能通过使用 E(W) 权限创建的目录的智能卡微型驱动程序接口。
-   不能通过更改文件或目录的权限而无需删除并重新创建文件或目录的智能卡微型驱动程序接口。
-   不能通过创建可以由管理员拥有的私钥文件的智能卡微型驱动程序接口或通过未经身份验证的用户。
-   不能通过创建 PIN 文件 （E(X)、 U(W) 和 A(W)) 在卡上智能卡微型驱动程序接口。
-   不能通过查询目录访问条件的智能卡微型驱动程序接口。
-   才可以通过创建文件的访问权限的子集提供的条件组合的智能卡微型驱动程序接口。

 

 





