---
title: reg
description: Reg 扩展显示和搜索注册表数据。
keywords:
- reg Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- reg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e6add1d5556afef74e1ef38d7450021c6f7c877
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815489"
---
# <a name="reg"></a>!reg


**！ Reg** 扩展显示和搜索注册表数据。

```dbgcmd
!reg {querykey|q} FullKeyPath
!reg keyinfo HiveAddress KeyNodeAddress
!reg kcb Address 
!reg knode Address 
!reg kbody Address 
!reg kvalue Address 
!reg valuelist HiveAddress KeyNodeAddress 
!reg subkeylist HiveAddress KeyNodeAddress  
!reg baseblock HiveAddress 
!reg seccache HiveAddress 
!reg hashindex [HiveAddress]HashKey
!reg openkeys {HiveAddress|0}
!reg openhandles {HiveAddress|0} 
!reg findkcb FullKeyPath 
!reg hivelist 
!reg viewlist HiveAddress 
!reg freebins HiveAddress 
!reg freecells BinAddress 
!reg dirtyvector HiveAddress 
!reg cellindex HiveAddress Index
!reg freehints HiveAddress Storage Display 
!reg translist {RmAddress|0}
!reg uowlist TransactionAddress
!reg locktable KcbAddress ThreadAddress
!reg convkey KeyPath
!reg postblocklist
!reg notifylist
!reg ixlock LockAddress
!reg dumppool [s|r]
```

## <a name="span-idddk__reg_dbgspanspan-idddk__reg_dbgspanparameters"></a><span id="ddk__reg_dbg"></span><span id="DDK__REG_DBG"></span>参数


<span id="_______querykeyq_FullKeyPath______"></span><span id="_______querykeyq_fullkeypath______"></span><span id="_______QUERYKEYQ_FULLKEYPATH______"></span>{**查询密钥** |**q**} * * * * * * *FullKeyPath*   
如果已缓存密钥，则显示密钥的子项和值。 *FullKeyPath* 指定完整的密钥路径。

<span id="_____________keyinfo_HiveAddress_KeyNodeAddress"></span><span id="_____________keyinfo_hiveaddress_keynodeaddress"></span><span id="_____________KEYINFO_HIVEADDRESS_KEYNODEADDRESS"></span>**keyinfo** *HiveAddress*  ****  *KeyNodeAddress*  
显示密钥节点的子项和值。 *HiveAddress* 指定 hive 的地址。 *KeyNodeAddress* 指定密钥节点的地址。

<span id="_______kcb_______Address______"></span><span id="_______kcb_______address______"></span><span id="_______KCB_______ADDRESS______"></span>**kcb**  **** *地址*   
显示注册表项控制块。 *Address* 指定密钥控制块的地址。

<span id="_______knode_______Address______"></span><span id="_______knode_______address______"></span><span id="_______KNODE_______ADDRESS______"></span>**knode**  **** *地址*   
显示注册表项节点结构。 *Address* 指定密钥节点的地址。

<span id="_______kbody_______Address______"></span><span id="_______kbody_______address______"></span><span id="_______KBODY_______ADDRESS______"></span>**kbody**  **** *地址*   
显示注册表项正文结构。 *Address* 指定密钥正文的地址。  (注册表项体是与句柄关联的实际对象。 ) 

<span id="_______kvalue_______Address______"></span><span id="_______kvalue_______address______"></span><span id="_______KVALUE_______ADDRESS______"></span>**kvalue**  **** *地址*   
显示注册表项的值结构。 *Address* 指定值的地址。

<span id="_______valuelist_______HiveAddress_KeyNodeAddress______"></span><span id="_______valuelist_______hiveaddress_keynodeaddress______"></span><span id="_______VALUELIST_______HIVEADDRESS_KEYNODEADDRESS______"></span>**valuelist**  **** *HiveAddress*  **** *KeyNodeAddress*   
显示指定键节点中的值的列表。 *HiveAddress* 指定 hive 的地址。 *KeyNodeAddress* 指定密钥节点的地址。

<span id="subkeylist_______HiveAddress_KeyNodeAddress______"></span><span id="subkeylist_______hiveaddress_keynodeaddress______"></span><span id="SUBKEYLIST_______HIVEADDRESS_KEYNODEADDRESS______"></span>**subkeylist**  **** *HiveAddress*  **** *KeyNodeAddress*   
显示指定键节点的子项列表。 *HiveAddress* 指定 hive 的地址。 *KeyNodeAddress* 指定密钥节点的地址。

<span id="_______baseblock_______HiveAddress______"></span><span id="_______baseblock_______hiveaddress______"></span><span id="_______BASEBLOCK_______HIVEADDRESS______"></span>**baseblock**  **** *HiveAddress*   
显示 hive (的基块，也称为 *hive 标头*) 。 *HiveAddress* 指定 hive 的地址。

<span id="_______seccache_______HiveAddress______"></span><span id="_______seccache_______hiveaddress______"></span><span id="_______SECCACHE_______HIVEADDRESS______"></span>**seccache**  **** *HiveAddress*   
显示 hive 的安全性缓存。 *HiveAddress* 指定 hive 的地址。

<span id="_______hashindex_______HiveAddress_HashKey______"></span><span id="_______hashindex_______hiveaddress_hashkey______"></span><span id="_______HASHINDEX_______HIVEADDRESS_HASHKEY______"></span>**hashindex**  ****  hashindex \[*HiveAddress* \] HiveAddress  **** *HashKey*   
计算哈希键的哈希索引条目。 *HiveAddress* 指定 hive 的地址。 *HashKey* 指定密钥。

**请注意**，如果目标计算机运行的是 Windows 7 或更高版本，则 *HiveAddress* 是必需的。



<span id="_______openkeys_HiveAddress0_"></span><span id="_______openkeys_hiveaddress0_"></span><span id="_______OPENKEYS_HIVEADDRESS0_"></span>**sys.openkeys** {*HiveAddress* | **0**}   
显示 hive 中的所有打开的键。 *HiveAddress* 指定 hive 的地址。 如果改为使用零，则显示整个注册表哈希表;此表包含注册表中的所有打开的项。

<span id="_______findkcb_______FullKeyPath______"></span><span id="_______findkcb_______fullkeypath______"></span><span id="_______FINDKCB_______FULLKEYPATH______"></span>**findkcb**  **** *FullKeyPath*   
显示与注册表路径对应的注册表项控制块。 *FullKeyPath* 指定完整的密钥路径;此路径必须存在于哈希表中。

<span id="_______hivelist______"></span><span id="_______HIVELIST______"></span>**hivelist**   
显示系统中所有配置单元的列表，以及有关每个配置单元的详细信息。

<span id="_______viewlist_______HiveAddress______"></span><span id="_______viewlist_______hiveaddress______"></span><span id="_______VIEWLIST_______HIVEADDRESS______"></span>**viewlist**  **** *HiveAddress*   
显示 hive 的所有固定和映射视图，以及每个视图的详细信息。 *HiveAddress* 指定 hive 的地址。

<span id="_______freebins_______HiveAddress______"></span><span id="_______freebins_______hiveaddress______"></span><span id="_______FREEBINS_______HIVEADDRESS______"></span>**freebins**  **** *HiveAddress*   
显示 hive 的所有可用箱，其中包含每个储箱的详细信息。 *HiveAddress* 指定 hive 的地址。

<span id="_______freecells_______BinAddress______"></span><span id="_______freecells_______binaddress______"></span><span id="_______FREECELLS_______BINADDRESS______"></span>**freecells**  **** *BinAddress*   
循环访问一个 bin 并显示其中所有可用的单元格。 *BinAddress* 指定 bin 的地址。

<span id="_______dirtyvector_______HiveAddress______"></span><span id="_______dirtyvector_______hiveaddress______"></span><span id="_______DIRTYVECTOR_______HIVEADDRESS______"></span>**dirtyvector**  **** *HiveAddress*   
显示 hive 的脏向量。 *HiveAddress* 指定 hive 的地址。

<span id="_______cellindex_______HiveAddress_Index______"></span><span id="_______cellindex_______hiveaddress_index______"></span><span id="_______CELLINDEX_______HIVEADDRESS_INDEX______"></span>**cellindex**  **** *HiveAddress*  **** *索引*   
显示 hive 中单元格的虚拟地址。 *HiveAddress* 指定 hive 的地址。 *Index* 指定单元格索引。

<span id="_____________freehints_HiveAddress_Storage_Display"></span><span id="_____________freehints_hiveaddress_storage_display"></span><span id="_____________FREEHINTS_HIVEADDRESS_STORAGE_DISPLAY"></span>**freehints** *HiveAddress*  ****  *存储*  ****  *显示*  
显示免费提示信息。

<span id="_____________translist_RmAddress0"></span><span id="_____________translist_rmaddress0"></span><span id="_____________TRANSLIST_RMADDRESS0"></span>**translist** {*RmAddress* | **0**}  
显示 RM 中活动事务的列表。 *RmAddress* 指定 RM 的地址。

<span id="_____________uowlist_TransactionAddress"></span><span id="_____________uowlist_transactionaddress"></span><span id="_____________UOWLIST_TRANSACTIONADDRESS"></span>**uowlist** *TransactionAddress*  
显示附加到事务的 UoWs 的列表。 *TransactionAddress* 指定事务的地址。

<span id="_____________locktable_KcbAddress_ThreadAddress"></span><span id="_____________locktable_kcbaddress_threadaddress"></span><span id="_____________LOCKTABLE_KCBADDRESS_THREADADDRESS"></span>**locktable** *KcbAddress* *ThreadAddress*  
显示相关的锁定表内容。

<span id="_____________convkey_KeyPath"></span><span id="_____________convkey_keypath"></span><span id="_____________CONVKEY_KEYPATH"></span>**convkey** *KeyPath*  
显示密钥路径的哈希键。

<span id="_____________postblocklist"></span><span id="_____________POSTBLOCKLIST"></span>**postblocklist**  
显示已 postblocks 发布的线程的列表。

<span id="_____________notifylist"></span><span id="_____________NOTIFYLIST"></span>**notifylist**  
显示系统中的通知块的列表。

<span id="_____________ixlock_LockAddress"></span><span id="_____________ixlock_lockaddress"></span><span id="_____________IXLOCK_LOCKADDRESS"></span>**ixlock** *LockAddress*  
显示意向锁的所有权。 *LockAddress* 指定锁的地址。

<span id="_______dumppool_sr"></span><span id="_______DUMPPOOL_SR"></span>**dumppool** \[**s** |**r**\]  
显示注册表分配的分页池。 如果 **指定了，** 则会将注册表页的列表保存到临时文件中。 如果指定 **r** ，则从以前保存的临时文件还原注册表页列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册表及其组件的信息，请参阅 *Microsoft Windows 内部机制* （标记 Russinovich 和 David）。 

<a name="remarks"></a>备注
-------

示例如下。 首先使用 **！ reg hivelist** 获取 hive 地址的列表。

```dbgcmd
00: kd> !reg hivelist
## 

## |     HiveAddr     |Stable Length|    Stable Map    |Volatile Length|    Volatile Map    |MappedViews|PinnedViews|U(Cnt)|     BaseBlock     | FileName 

| fffff8a000014010 |       1000  | fffff8a0000140b0 |       1000    |  fffff8a000014328  |     0| fffff8a00001e000  | <NONAME>
| fffff8a000028010 |     a15000  | fffff8a00002e000 |      1a000    |  fffff8a000028328  |     0| fffff8a000029000  | SYSTEM
| fffff8a00004f010 |      14000  | fffff8a00004f0b0 |       c000    |  fffff8a00004f328  |     0| fffff8a000050000  | <NONAME>
| fffff8a000329010 |       6000  | fffff8a0003290b0 |          0    |  0000000000000000  |     0| fffff8a00032f000  | Device\HarddiskVolume1\Boot\BCD
| fffff8a0002f2010 |    4255000  | fffff8a0006fa000 |       6000    |  fffff8a0002f2328  |     0| fffff8a00036c000  | emRoot\System32\Config\SOFTWARE
| fffff8a000df0010 |      f7000  | fffff8a000df00b0 |       1000    |  fffff8a000df0328  |     0| fffff8a000df1000  | temRoot\System32\Config\DEFAULT
| fffff8a0010f8010 |       9000  | fffff8a0010f80b0 |       1000    |  fffff8a0010f8328  |     0| fffff8a0010f9000  | emRoot\System32\Config\SECURITY
| fffff8a001158010 |       7000  | fffff8a0011580b0 |          0    |  0000000000000000  |     0| fffff8a001159000  | \SystemRoot\System32\Config\SAM
| fffff8a00124b010 |      24000  | fffff8a00124b0b0 |          0    |  0000000000000000  |     0| fffff8a00124c000  | files\NetworkService\NTUSER.DAT
| fffff8a0012df220 |      b7000  | fffff8a0012df2c0 |          0    |  0000000000000000  |     0| fffff8a0012e6000  | \SystemRoot\System32\Config\BBI
| fffff8a001312220 |      26000  | fffff8a0013122c0 |          0    |  0000000000000000  |     0| fffff8a00117e000  | rofiles\LocalService\NTUSER.DAT
| fffff8a001928010 |      64000  | fffff8a0019280b0 |       3000    |  fffff8a001928328  |     0| fffff8a00192b000  | User.MYTESTCOMPUTER2\ntuser.dat
| fffff8a001b9b010 |     203000  | fffff8a001bc4000 |          0    |  0000000000000000  |     0| fffff8a001b9c000  | \Microsoft\Windows\UsrClass.dat
| fffff8a001dc0010 |      30000  | fffff8a001dc00b0 |          0    |  0000000000000000  |     0| fffff8a001dc2000  | Volume Information\Syscache.hve
## | fffff8a0022dc010 |     175000  | fffff8a0022dc0b0 |          0    |  0000000000000000  |     0| fffff8a0022dd000  | \AppCompat\Programs\Amcache.hve
```

在前面的输出中使用第三个 hive 地址 (fffff8a00004f010) 作为 **！ reg sys.openkeys** 的参数。

```dbgcmd
0: kd> !reg openkeys fffff8a00004f010

# Hive: \REGISTRY\MACHINE\HARDWARE

Index e9:    3069276d kcb=fffff8a00007eb98 cell=00000220 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM
Index 101:   292eea1f kcb=fffff8a00007ecc0 cell=000003b8 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM\MULTIFUNCTIONADAPTER
Index 140:   d927b0d4 kcb=fffff8a00007ea70 cell=000001a8 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION
Index 160:   96d26a30 kcb=fffff8a00007e6f8 cell=00000020 f=002c0000 \REGISTRY\MACHINE\HARDWARE

# 0x4 keys found
```

使用前面输出中的第一个完整密钥路径 (\\ 注册表 \\ 计算机 \\ 硬件 \\ 描述 \\ 系统) 作为 **！ reg 查询密钥** 的参数。

```dbgcmd
0: kd> !reg querykey \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM

Found KCB = fffff8a00007eb98 :: \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM

Hive         fffff8a00004f010
KeyNode      fffff8a000054224

[SubKeyAddr]         [SubKeyName]
fffff8a000060244     CentralProcessor
fffff8a00006042c     FloatingPointProcessor
fffff8a0000543bc     MultifunctionAdapter

[SubKeyAddr]         [VolatileSubKeyName]
fffff8a000338d8c     BIOS
fffff8a0002a2e4c     VideoAdapterBusses

 Use '!reg keyinfo fffff8a00004f010 <SubKeyAddr>' to dump the subkey details

[ValueType]         [ValueName]                   [ValueData]
REG_BINARY          Component Information         0x542AC - 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
REG_SZ              Identifier                    AT/AT COMPATIBLE
REG_FULL_RESOURCE_DESCRIPTORConfiguration Data            ff ff ff ff ff ff ff ff 00 00 00 00 02 00 00 00 05 00 00 00 18 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 00 ff 03 00 00 3f 00 fe 00 02 00 81 00 fe 03 00 00 3f 00 fe 00 02 00 05 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 0c 00 00 00 04 00 
REG_SZ              SystemBiosDate                07/18/07
REG_MULTI_SZ        SystemBiosVersion             HPQOEM - 20070718\0\0
REG_SZ              VideoBiosDate                 03/23/20
REG_MULTI_SZ        VideoBiosVersion              Hardware Version 0.0\0\0
```

以下是另一个示例：

```dbgcmd
kd> !reg hivelist
## 

## | HiveAddr |Stable Length|Stable Map|Volatile Length|Volatile Map|MappedViews|PinnedViews|U(Cnt)| BaseBlock | FileName 

| e16e7428 |       2000  | e16e7484 |          0    |  00000000  |        1  |        0  |     0| e101f000  | \Microsoft\Windows\UsrClass.dat
| e1705a78 |      77000  | e1705ad4 |       1000    |  e1705bb0  |       30  |        0  |     0| e101c000  | ttings\Administrator\ntuser.dat
| e13d4b88 |     814000  | e146a000 |       1000    |  e13d4cc0  |      255  |        0  |     0| e1460000  | emRoot\System32\Config\SOFTWARE
| e13ad008 |      23000  | e13ad064 |       1000    |  e13ad140  |        9  |        0  |     0| e145e000  | temRoot\System32\Config\DEFAULT
| e13b3b88 |       a000  | e13b3be4 |       1000    |  e13b3cc0  |        3  |        0  |     0| e145d000  | emRoot\System32\Config\SECURITY
| e142d008 |       5000  | e142d064 |          0    |  00000000  |        2  |        0  |     0| e145f000  | <UNKNOWN>
| e11e3628 |       4000  | e11e3684 |       3000    |  e11e3760  |        0  |        0  |     0| e11e4000  | <NONAME>
| e10168a8 |     1c1000  | e1016904 |      15000    |  e10169e0  |       66  |        0  |     0| e1017000  | SYSTEM
## | e10072c8 |       1000  | e1007324 |          0    |  00000000  |        0  |        0  |     0| e1010000  | <NONAME>


kd> !reg hashindex e16e7428

CmpCacheTable = e100a000

Hash Index[e16e7428] : 5ac
Hash Entry[e16e7428] : e100b6b0

kd> !reg openkeys e16e7428

Index 68:  7bab7683 kcb=e13314f8 cell=00000740 f=00200004 \REGISTRY\USER\S-1-5-21-1715567821-413027322-527237240-500_Classes\CLSID
Index 7a1:  48a30288 kcb=e13a3738 cell=00000020 f=002c0004 \REGISTRY\USER\S-1-5-21-1715567821-413027322-527237240-500_Classes
```

若要显示格式化的注册表项信息，请改用 [**！ dreg**](-dreg.md) 扩展。









