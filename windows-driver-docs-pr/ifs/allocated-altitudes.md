---
title: 分配的等级
description: 分配的等级
ms.assetid: EC1993FB-5219-4C0C-A76A-05937A461C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703112d39982e4a4fef84d62fbcbed2f38a16131
ms.sourcegitcommit: 5e257e7d54d77649b4981a55a7d61676a3b25f00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064152"
---
# <a name="allocated-altitudes"></a>分配的等级

开发到筛选器管理器模型的文件系统微筛选器驱动程序必须具有唯一的标识符，该标识符被称为定义其相对于文件系统堆栈中存在的其他 minifilters 的位置的高度。 微微筛选器根据微微筛选器要求和加载顺序组分配。

若要请求微筛选器海拔数，请参阅[微筛选器请求](minifilter-altitude-request.md)。

下面列出了以下每个加载顺序组的最新分配数。

## <a name="span-id420000_-_429999__filterspanspan-id420000_-_429999__filterspanspan-id420000_-_429999__filterspan420000---429999-filter"></a><span id="420000_-_429999__Filter"></span><span id="420000_-_429999__filter"></span><span id="420000_-_429999__FILTER"></span>420000-429999：筛选器

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntoskrnl.exe | 425500 | Microsoft |
| ntoskrnl.exe | 425000 | Microsoft |

## <a name="span-id400000_-_409999__fsfilter_topspanspan-id400000_-_409999__fsfilter_topspanspan-id400000_-_409999__fsfilter_topspan400000---409999-fsfilter-top"></a><span id="400000_-_409999__FSFilter_Top"></span><span id="400000_-_409999__fsfilter_top"></span><span id="400000_-_409999__FSFILTER_TOP"></span>400000-409999： FSFilter Top

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcnfs | 409900 | Microsoft |
| bindflt | 409800 | Microsoft |
| cldflt | 409500 | Microsoft |
| iorate | 409010 | Microsoft |
| ioqos | 409000 | Microsoft |
| fsdepends | 407000 | Microsoft |
| sftredir | 406000 | Microsoft |
| node.js | 405000 | Microsoft |
| 跟踪器 .sys | 404910 | Acronis |
| csvnsflt | 404900 | Microsoft |
| csvflt | 404800 | Microsoft |
| Uev. AgentDriver | 404710 | Microsoft |
| AppvVfs | 404700 | Microsoft |
| CCFFilter | 404600 | Microsoft |
| dciogrd | 402010 | Datacloak 技术 |
| Dewdrv | 402000 | Dell 技术 |
| zsusbstorfilt | 401910 | Zshield Inc。 |
| eaw | 401900 | Raytheon 网络解决方案 |
| TVFsfilter | 401800 | TrustView |
| KKDiskProtecter | 401700 | Goldmsg |
| AgentComm | 401600 | Trustwave 控股 Inc。 |
| rvsavd | 401500 | CJSC Returnil 软件 |
| DGMinFlt | 401410 | 数字保护者 Inc。 |
| dgdmk | 401400 | Verdasys Inc。 |
| tusbstorfilt | 401300 | SimplyCore LLC |
| pcgenfam | 401200 | Soluto |
| atrsdfw | 401100 | Altiris |
| tpfilter | 401000 | RedPhone 安全性 |
| MBIG2Prot | 400920 | Malwarebytes Inc。 |
| mbamwatchdog | 400900 | Malwarebytes 公司 |
| DSESafeCtrlDrv | 400803 | 上海 Eff-软 IT |
| edevmon | 400800 | ESET spol。 s r.o。 |
| vmwflstor | 400700 | VMware，Inc。 |
| TsQBDrv | 400600 | 腾讯技术 |
| WRAEKernel | 400500 | Webroot Inc。 |

## <a name="span-id360000_-_389999__fsfilter_activity_monitorspanspan-id360000_-_389999__fsfilter_activity_monitorspanspan-id360000_-_389999__fsfilter_activity_monitorspan360000---389999-fsfilter-activity-monitor"></a><span id="360000_-_389999__FSFilter_Activity_Monitor"></span><span id="360000_-_389999__fsfilter_activity_monitor"></span><span id="360000_-_389999__FSFILTER_ACTIVITY_MONITOR"></span>360000-389999： FSFilter 活动监视器

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| klboot | 389510 | Kaspersky 等实验室 |
| klfdefsf | 389500 | Kaspersky 等实验室 |
| CBFSFilter2017 | 389250 | SecureLink Inc。 |
| NWEDriver | 389240 | Dell 技术 |
| cytmon | 389230 | Cytrence Inc。 |
| SophosED | 389220 | Sophos |
| MonsterK | 389210 | Somma Inc。 |
| IFS64 | 389200 | Ashampoo 开发 |
| TSTFilter | 389190 | ThinScale 技术 |
| VrnsFilter | 389180 | Varonis 有限公司 |
| lrtp | 389170 | 联想北京 |
| ipcomfltr | 389160 | Bluzen Inc。 |
| SvCBT | 389150 | Spharsoft 技术 |
| mbamshuriken | 389140 | Malwarebytes |
| ContainerMonitor | 389130 | 浅绿安全 |
| SaMFlt | 389120 | DreamCrafts |
| RuiMinispy | 389117 | RuiGuard 有限公司 |
| RuiFileAccess | 389115 | RuiGuard 有限公司 |
| RuiEye | 389113 | RuiGuard 有限公司 |
| RuiMachine | 389111 | RuiGuard 有限公司 |
| windd | 389110 | Comae 技术 |
| cbfsfilter2017 | 389105 | Basein 网络 |
| taobserveflt | 389100 | ThinAir Labs Inc。 |
| vollock | 389092 | Man 技术 Inc。 |
| drbdlock | 389090 | Man 技术 Inc。 |
| dcfsgrd | 389085 | Datacloak 技术 |
| hsmltmon | 389080 | Hitachi 解决方案 |
| AternityRegistryHook | 389070 | Aternity 有限公司 |
| MozyNextFilter | 389068 | Carbonite Inc。 |
| MozyCorpFilter | 389067 | Carbonite Inc。 |
| MozyEntFilter | 389066 | Carbonite Inc。 |
| MozyOEMFilter | 389065 | Carbonite Inc。 |
| MozyEnterpriseFilter | 389064 | Carbonite Inc。 |
| MozyProFilter | 389063 | Carbonite Inc。 |
| MozyHomeFilter | 389062 | Carbonite Inc。 |
| BDSFilter | 389061 | Carbonite Inc。 |
| CSBFilter | 389060 | Carbonite Inc。 |
| ChemometecFilter | 389050 | ChemoMetec |
| SentinelMonitor | 389040 | SentinelOne |
| DhWatchdog | 389030 | Microsoft |
| edrsensor | 389025 | Bitdefender SRL |
| bdprivmon | 389022 | Bitdefender SRL |
| NpEtw | 389020 | Koby Kahane |
| OczMiniFilter | 389010 | OCZ 存储 |
| ielcp | 389004 | Intel Corporation |
| IESlp | 389002 | Intel Corporation |
| IntelCAS | 389000 | Intel Corporation |
| boxifier | 388990 | Kenubi |
| SamsungRapidFSFltr | 388980 | NVELO Inc。 |
| drsfile | 388970 | MRY Inc。 |
| CbFltFs4 | 388966 | Simopro 技术 |
| CrUnCopy | 388964 | Shenzhen CloudRiver |
| aictracedrv_am | 388960 | AI 咨询 |
| fiopolicyfilter | 388954 | SanDisk Inc。 |
| fcontrol | 388950 | SODATSW spol. s r.o。 |
| qfilter.sys | 388940 | 仲裁实验室 |
| Redlight | 388930 | Trustware 有限公司 |
| eps | 388920 | Lumension |
| VHDTrack | 388915 | Intronis Inc。 |
| VHDDelta | 388912 | Niriva LLC |
| FSTrace | 388910 | Niriva LLC |
| YahooStorage | 388900 | Yahoo 日本公司 |
| KeWF | 388890 | KEBA AG |
| epregflt | 388888 | 检查点软件 |
| epklib | 388886 | 检查点软件 |
| zsfprt | 388880 | k4solution Co。 |
| dsflt | 388876 | cEncrypt |
| bfaccess | 388872 | bitFence Inc。 |
| xcpl | 388870 | X 云系统 |
| DCFAFilter | 388866 | ManageEngine Zoho |
| RMPHVMonitor | 388865 | ManageEngine Zoho |
| FAPMonitor | 388864 | ManageEngine Zoho |
| EaseFlt | 388860 | EaseVault 技术 Inc。 |
| rpwatcher | 388855 | 最佳安全性 |
| sieflt | 388852 | 快速修复技术 Pvt。 Ltd. |
| cssdlp | 388851 | 快速修复技术 Pvt。 Ltd. |
| cssdlp | 388850 | CoSoSys |
| INISBDrv64 | 388840 | Initech Inc。 |
| config.sys | 388831 | Fitsec 有限公司 |
| SandDriver | 388830 | Fitsec 有限公司 |
| dskmn | 388820 | Honeycomb 技术 |
| xkfsfd | 388810 | Jiransoft，有限公司 |
| pcpifd | 388800 | Jiransoft，有限公司 |
| NNTInfo | 388790 | 新的网络技术有限 |
| FsMonitor | 388780 | IBM |
| CVCBT | 388770 | CommVault Systems，Inc。 |
| AwareCore | 388760 | TaaSera Inc。 |
| laFS | 388750 | NetworkProfi 有限公司。 |
| fsnk | 388740 | SoftPerfect 研究 |
| RGNT | 388730 | HFN Inc。 |
| fltRs329 | 388720 | 安全的环球公司 |
| ospmon | 388710 | SC ODEKIN 解决方案 SRL |
| edsigk | 388700 | 企业数据解决方案，Inc。 |
| fiometer | 388692 | 合成-io |
| dcSnapRestore | 388690 | 合成-io |
| fam | 388680 | 快速修复技术 Pvt。 Ltd. |
| vidderfs | 388675 | Vidder Inc。 |
| Tritiumfltr | 388670 | Tritium Inc。 |
| HexisFSMonitor | 388660 | Hexis 网络解决方案 |
| BlackbirdFSA | 388650 | BeyondTrust Inc。 |
| TMUMS | 388642 | 走向微 Inc。 |
| hfileflt | 388640 | 走向微 Inc。 |
| TMUMH | 388630 | 走向微 Inc。 |
| AcDriver | 388620 | 走向微，Inc。 |
| SakFile | 388610 | 走向微，Inc。 |
| SakMFile | 388600 | 走向微，Inc。 |
| rsfdrv | 388580 | Clonix Co |
| alcapture | 388570 | 代表太空飞船数字 Pty 有限公司 |
| kmNWCH | 388560 | IGLOO SECURITY，Inc。 |
| ISIRMFmon | 388550 | ALPS 系统 INTEGRATION CO。 |
| EsProbe | 388542 | Stormshield |
| heimdall | 388540 | Arkoon 网络安全 |
| thetta | 388532 | Syncopate |
| thetta | 388531 | Syncopate |
| thetta | 388530 | Syncopate |
| DTPL | 388520 | 连接班次公司 |
| CyOptics | 388514 | Cylance Inc。 |
| CyProtectDrv32 | 388510 | Cylance Inc。 |
| CyProtectDrv64 | 388510 | Cylance Inc。 |
| tbfsfilt | 388500 | 第三 Bucket-brigade |
| IvAppMon | 388491 | Ivanti |
| LDSecDrv | 388490 | LANDESK 软件 |
| SGResFlt | 388480 | Samsung SDS 有限公司 |
| CwMem2k64 | 388470 | ApSoft |
| axfltdrv | 388460 | Axact Pvt 有限公司 |
| RMDiskMon | 388450 | Qingdao Ruanmei 网络技术 Co。 |
| diskactmon | 388440 | Qingdao Ruanmei 网络技术 Co。 |
| Codex | 388430 | GameHi Co。 |
| CatMF | 388420 | Logichron Inc。 |
| RW7FsFlt | 388410 | PJSC KP VTI |
| aswSP | 388401 | Avast 软件 |
| aswFsBlk | 388400 | ALWIL 软件 |
| ThreatStackFIM | 388380 | 威胁堆栈 |
| BOsCmFlt | 388370 | Barkly 保护 Inc。 |
| BOsFsFltr | 388370 | Barkly 保护 Inc。 |
| FeKern | 388360 | FireEye Inc。 |
| libwamf | 388350 | OPSWAT Inc。 |
| SZEDRDrv | 388346 | SaferZone Co。 |
| szardrv | 388345 | SaferZone Co。 |
| szpcmdrv | 388341 | SaferZone Co。 |
| szdfmdrv | 388340 | SaferZone Co。 |
| szdfmdrv_usb | 388331 | SaferZone Co。 |
| sprtdrv | 388330 | SaferZone Co。 |
| SWFsFltrv2 | 388321 | Solarwinds LLC |
| SWFsFltr | 388320 | Solarwinds LLC |
| flashaccelfs | 388310 | 网络设备 |
| changelog | 388300 | 网络设备 |
| stcvsm | 388250 | StorageCraft 技术 |
| aUpDrv | 388240 | ITSTATION Inc。 |
| fshs | 388222 | F-安全 |
| fshs | 388221 | F-安全 |
| fsatp | 388220 | F-安全 |
| SecdoDriver | 388210 | Secdo |
| TGFSMF | 388200 | Tetraglyph 技术 |
| evscase | 388100 | 三月 h Software 有限公司 |
| VSScanner | 388050 | VoodooSoft |
| HDRansomOffDrv | 388044 | Heilig 防卫 LLC |
| HDCorrelateFDrv | 388042 | Heilig 防卫 LLC |
| HDFileMon | 388040 | Heilig 防卫 LLC |
| tsifilemon | 388012 | 对讲机 Inc。 |
| MarSpy | 388010 | 对讲机 Inc。 |
| AGSysLock | 388002 | AppGuard LLC |
| AGSecLock | 388001 | AppGuard LLC |
| BrnFileLock | 388000 | 蓝色凸网络 |
| BrnSecLock | 387990 | 蓝色凸网络 |
| LCmPrintMon | 387978 | YATEM |
| LCgAdMon | 387977 | YATEM |
| LCmAdMon | 387976 | YATEM |
| LCgFileMon | 387975 | YATEM |
| LCmFile | 387974 | YATEM |
| LCgFile | 387972 | YATEM |
| LCmFileMon | 387970 | YATEM |
| IridiumSwitch | 387960 | Confio |
| scensemon | 387950 | AppiXoft |
| ruaff | 387940 | RUNEXY |
| bbfilter | 387930 | derivo GmbH |
| Bfmon | 387920 | 百度（香港特别行政区）受限 |
| bdsysmon | 387912 | 百度 Online 网络 |
| BdRdFolder | 387910 | 百度（北京） |
| mlsaff | 387901 | RUNEXY |
| pscff | 387900 | Weing，有限公司 |
| fcnotify | 387880 | TCXA 有限公司。 |
| aaf | 387860 | Actifio Inc。 |
| gddcv | 387840 | G 数据软件 AG |
| wgfile | 387820 | 橙色 WERKS Inc。 |
| zesfsmf | 387800 | Novell |
| uamflt | 387700 | Sevtechnotrans |
| ehdrv | 387600 | ESET、spol。 s r.o。 |
| DattoFSF | 387560 | Datto Inc。 |
| FileSystemCBT | 387550 | Rubrik Inc。 |
| Snilog | 387500 | Systemneeds，Inc。 |
| tss | 387400 | Tiversa Inc。 |
| LmDriver | 387390 | 软 Kft。 |
| WDCFilter | 387330 | Interset Inc。 |
| altcbt | 387320 | Altaro 有限公司。 |
| bapfecpt | 387310 | BitArmor Systems，Inc。 |
| bamfltr | 387300 | BitArmor Systems，Inc。 |
| TrustedEdgeFfd | 387200 | FileTek，Inc。 |
| MRxGoogle | 387100 | Google，Inc。 |
| YFSDR.系统 | 387010 | Yokogawa R & L Corp |
| YFSD.系统 | 387000 | Yokogawa R & L Corp |
| YFSRD | 386990 | Yokogawa R & L Corp |
| psgfoctrl | 386990 | Yokogawa R & L Corp |
| psgdflt | 386980 | Yokogawa R & L Corp |
| USBPDH.系统 | 386901 | 高级计算开发中心 |
| pecfilter | 386900 | C-DAC 海得拉巴 |
| GKPFCB | 386810 | INCA Internet Co。 |
| GKPFCB64 | 386810 | INCA Internet Co。 |
| 32位 TkPcFtCb | 386800 | INCA Internet 有限公司。 |
| 64位 TkPcFtCb64 | 386800 | INCA Internet 有限公司。 |
| bmregdrv | 386731 | Yandex LLC |
| bmfsdrv | 386730 | Yandex LLC |
| CarbonBlackK | 386720 | Bit9 Inc。 |
| ScAuthFSFlt | 386710 | 安全代码 LLC |
| ScAuthIoDrv | 386700 | 安全代码 LLC |
| mfeaskm | 386610 | McAfee Inc。 |
| mfencfilter | 386600 | McAfee |
| WinFLAHdrv | 386540 | NewSoftwares&#x2024;Net，inc。 |
| WinFLAdrv | 386530 | NewSoftwares&#x2024;Net，inc。 |
| WinDBdrv | 386520 | NewSoftwares&#x2024;Net，inc。 |
| WinFLdrv | 386510 | NewSoftwares&#x2024;Net，inc。 |
| WinFPdrv | 386500 | NewSoftwares&#x2024;Net，inc。 |
| SkyWPDrv | 386435 | 天空有限公司。 |
| SkyRGDrv | 386431 | 天空有限公司。 |
| SkyAMDrv | 386430 | 天空有限公司。 |
| SheedSelfProtection | 386421 | SheedSoft 有限公司 |
| arta | 386420 | SheedSoft 有限公司。 |
| ApexSqlFilterDriver | 386410 | ApexSQL LLC |
| stflt | 386400 | Xacti |
| tbrdrv | 386390 | 爬网程序组 |
| WinTeonMiniFilter | 386320 | Dmitry Stefankov |
| 雨刮器 | 386310 | Dmitry Stefankov |
| DevMonMiniFilter | 386300 | Dmitry Stefankov |
| VMWVvpfsd | 386200 | VMware，Inc。 |
| RTOLogon （已重命名） | 386200 | VMware，Inc。 |
| Code42Filter | 386190 | Code42 |
| ConduantFSFltr | 386180 | Conduant 公司 |
| KtFSFilter | 386170 | Keysight 技术 |
| FileGuard | 386140 | RES 软件 |
| NetGuard | 386130 | RES 软件 |
| RegGuard | 386120 | RES 软件 |
| ImgGuard | 386110 | RES 软件 |
| AppGuard | 386100 | RES 软件 |
| RuiDiskFs | 386030 | RuiGuard 有限公司 |
| minitrc | 386020 | 受保护网络 |
| cpepmon | 386010 | 检查点软件 |
| CGWMF | 386000 | NetIQ |
| ISRegFlt | 385990 | Flexera Software Inc。 |
| ISRegFlt64 | 385990 | Flexera Software Inc。 |
| shdlpSf | 385970 | Comtrue 技术 |
| ctrPAMon | 385960 | Comtrue 技术 |
| shdlpMedia | 385950 | Comtrue 技术 |
| immflex | 385910 | Immidio B.V. |
| StegoProtect | 385900 | Stegosystems Inc。 |
| brfilter | 385890 | Bromium Inc。 |
| BrCow_x_x_x_x | 385889 | Bromium Inc。 |
| BemK | 385888 | Bromium Inc。 |
| secRMM | 385880 | Squadra 技术 |
| dgfilter | 385870 | DataGravity Inc。 |
| WFP_MRT | 385860 | FireEye Inc。 |
| klrsps | 385815 | Kaspersky 等实验室 |
| klsnsr | 385810 | Kaspersky 等实验室 |
| TaniumRecorderDrv | 385800 | Tanium |
| mssecflt | 385600 | Microsoft |
| Backupreader | 385500 | Microsoft |
| MsixPackagingToolMonitor | 385410 | Microsoft |
| AppVMon | 385400 | Microsoft |
| Dpmfilter.sys | 385300 | Microsoft |
| Procmon11 | 385200 | Microsoft |
| minispy-顶部 | 385100 | Microsoft |
| fdrtrace | 385001 | Microsoft |
| filetrace | 385000 | Microsoft |
| uwfreg | 384910 | Microsoft |
| uwfs | 384900 | Microsoft |
| locksmith | 384800 | Microsoft |
| winload.exe | 384700 | Microsoft |
| SFPMonitor-顶部 | 383350 | SonicWall Inc。 |
| FilrDriver | 383340 | 微聚焦 |
| rwchangedrv | 383330 | Rackware |
| airship-filter | 383320 | AIRWare 技术有限公司 |
| AeFilter | 383310 | Faronics 公司 |
| QQProtect | 383300 | 腾讯（Shenzhen） |
| QQProtectX64 | 383300 | 腾讯（Shenzhen） |
| KernelAgent32 | 383260 | ZoneFox |
| WRDWIZFILEPROT.系统 | 383251 | WardWiz |
| WRDWIZREGPROT.系统 | 383250 | WardWiz |
| groundling32 | 383200 | Dell Secureworks |
| groundling64 | 383200 | Dell Secureworks |
| avgtpx86 | 383190 | AVG 技术 CZ |
| avgtpx64 | 383190 | AVG 技术 CZ |
| DataNow_Driver | 383182 | AppSense 有限公司 |
| UcaFltDriver | 383180 | AppSense 有限公司 |
| YFSD2 | 383170 | Yokogawa Corpration |
| Kisknl | 383160 | kingsoft |
| MWatcher | 383150 | Neowiz 公司 |
| tsifilemon | 383140 | 对讲机 Inc。 |
| FIM-A | 383130 | eIQnetworks Inc。 |
| cFSfdrv | 383120 | Chaewool |
| ajfsprot | 383110 | Analytik Jena AG |
| isafermon | 383100 | ansi-cSMS |
| kfac | 383000 | 北京 JinChen Software。 |
| GUMHFilter | 382910 | Glarysoft 有限公司。 |
| PsAcFileAccessFilter | 382902 | FUJITSU 软件 |
| FJGSDis2 | 382900 | FUJITSU 有限 |
| secure_os | 382890 | FUJITSU 社会科学 |
| ibr2fsk | 382880 | FUJITSU 工程 |
| FJSeparettiFilterRedirect | 382860 | FUJITSU 有限 |
| Fsw31rj1 | 382855 | FUJITSU 有限 |
| da_ctl | 382850 | FUJITSU 有限 |
| zqFilter | 382800 | magrasoft 有限公司 |
| ntps_fa | 382700 | NTP 软件 |
| sConnect | 382600 | I-O 数据设备 |
| AdaptivaClientCache32 | 382500 | Adaptiva |
| AdaptivaclientCache64 | 382500 | Adaptiva |
| phantomd | 382440 | Veramine Inc。 |
| GoFSMF | 382430 | Gorizonty Rosta 有限公司 |
| SWCommFltr | 382420 | SnoopWall LLC |
| atflt | 382410 | Atlansys 软件 |
| amfd | 382400 | Atlansys 软件 |
| iSafeKrnl | 382390 | Elex 技术公司 |
| iSafeKrnlMon | 382380 | Elex 技术公司 |
| Qutmdrv | 382320 | 360软件（北京） |
| 360box | 382310 | Qihoo 360 |
| 360fsflt | 382300 | 北京 Qihoo 技术合作。 |
| scred | 382210 | SoftCamp Co。 |
| PDGenFam | 382200 | Soluto 有限公司 |
| MCFileMon64 （x64 系统） | 382100 | Sumitomo 电气有限公司。 |
| MCFileMon32 （x32 systems） | 382100 | Sumitomo 电气有限公司。 |
| RyGuard | 382050 | SHENZHEN UNNOO Information Techco。 |
| FileShareMon | 382040 | SHENZHEN UNNOO Information Techco。 |
| ryfilter | 382030 | SHENZHEN UNNOO Information Techco。 |
| secufile | 382020 | Shenzhen Unnoo 有限公司 |
| XiaobaiFs | 382010 | Shenzhen Unnoo 有限公司 |
| XiaobaiFsR | 382000 | Shenzhen Unnoo 有限公司 |
| TWBDCFilter | 381910 | Trustwave |
| VPDrvNt | 381900 | AhnLab，Inc。 |
| eetd32 | 381800 | Entrust Inc。 |
| eetd64 | 381800 | Entrust Inc。 |
| dnaFSMonitor | 381700 | Dtex 系统 |
| 2000上的 iwhlp2 | 381610 | InfoWatch |
| XP 上的 iwhlpxp | 381610 | InfoWatch |
| Vista 上的 iwhlp | 381610 | InfoWatch |
| iwdmfs | 381600 | InfoWatch |
| IronGateFD | 381500 | rubysoft |
| MagicBackupMonitor | 381400 | 幻 Softworks，Inc。 |
| Sonar.projectname | 381337 | IKARUS 安全性 |
| IPFilter | 381310 | Jinfengshuntai |
| MSpy | 381300 | Ladislav Zezula |
| 正在使用 | 381200 | 三月 h Software 有限公司 |
| qfmon | 381190 | 优质公司 |
| flyfs | 381160 | NEC 软 |
| serfs | 381150 | NEC 软 |
| hdrfs | 381140 | NEC 软 |
| UVMCIFSF | 381130 | NEC 公司 |
| ICFClientFlt | 381120 | 公司的 NEC 系统技术 |
| IccFileIoAd | 381110 | 公司的 NEC 系统技术 |
| IccFilterAudit | 381100 | NEC 系统技术 |
| IccFilterSc | 381090 | InfoCage |
| Sefo-顶部 | 381010 | Solusseum Inc。 |
| mtsvcdf | 381000 | CristaLink |
| SQLsafeFilterDriver | 380901 | Idera 软件 |
| IderaFilterDriver | 380900 | Idera |
| cbfsfilter2017 | 380850 | SN Systems 公司 |
| xhunter1 | 380800 | Wellbia&#x2024;com |
| iGuard | 380720 | i-保护 SAS |
| cbfltfs4 | 380715 | Nomadesk |
| cbfltfs4 | 380710 | 备份系统有限公司 |
| PkgFilter | 380700 | 可扩展的软件公司。 |
| snimg | 380600 | Softnext 技术 |
| SK .sys | 380520 | 热量软件 |
| mpxmon | 380510 | 正面技术 |
| filenamevalidator | 380502 | Infotecs |
| KC3 | 380500 | Infotecs |
| PLPOffDrv | 380492 | SK Infosec Co |
| ISFPDrv | 380491 | SK Infosec Co |
| ionmonwdrv | 380490 | SK Infosec Co |
| Sefo-中间 | 380480 | Solusseum Inc。 |
| sagntflt | 380470 | ShinNihonSystec Co |
| VrExpDrv | 380460 | Hauri Inc。 |
| srminifilterdrv | 380450 | Citrix 系统 |
| zzpensys | 380440 | Zhuan Zhuan Jing Shen |
| tedrdrv | 380430 | Palo Alto 网络 |
| fangcloud_autolock_driver | 380420 | 杭州 Yifangyun |
| CbSampleDrv | 380020 | Microsoft |
| CbSampleDrv | 380010 | Microsoft |
| CbSampleDrv | 380000 | Microsoft |
| simrep | 371100 | Microsoft |
| 更改 .sys | 370160 | Microsoft |
| delete_flt | 370150 | Microsoft |
| SmbResilFilter | 370140 | Microsoft |
| usbtest | 370130 | Microsoft |
| NameChanger | 370120 | Microsoft |
| failMount | 370110 | Microsoft |
| failAttach | 370100 | Microsoft |
| stest | 370090 | Microsoft |
| cdo | 370080 | Microsoft |
| ctx | 370070 | Microsoft |
| fmm | 370060 | Microsoft |
| cancelSafe | 370050 | Microsoft |
| message .sys | 370040 | Microsoft |
| 传递 .sys | 370030 | Microsoft |
| nullFilter | 370020 | Microsoft |
| 执行测试故障 | 370010 | Microsoft |
| minispy-中间 | 370000 | Microsoft |
| isecureflt | 368530 | iSecure 有限公司。 |
| SFPMonitor-中间 | 368520 | SonicWall Inc。 |
| wats_se | 368510 | Fujian Shen 特别行政区 |
| secure_os_mf | 368500 | HAURI |
| FileMonitor | 368470 | Cygna 实验室 |
| asiofms | 368460 | 鼓励技术 |
| cbfsfilter2017 | 368450 | 绝对软件 |
| FileHubAgent | 368440 | SmartFile LLC |
| nrcomgrdki | 368420 | NURILAB |
| nrcomgrdka | 368420 | NURILAB |
| nrpmonki | 368410 | NURILAB |
| nrpmonka | 368410 | NURILAB |
| nravwka | 368400 | NURILAB |
| bhkavki | 368390 | NURILAB |
| bhkavka | 368390 | NURILAB |
| docvmonk | 368380 | NURILAB |
| docvmonk64 | 368380 | NURILAB |
| InvProtectDrv | 368370 | Invincea |
| InvProtectDrv64 | 368370 | Invincea |
| browserMon | 368360 | Adtrustmedia |
| SfdFilter | 368350 | Sandoll 通信 |
| phdcbtdrv | 368340 | PHD 虚拟技术公司 |
| sysdiag | 368330 | HeroBravo 技术 |
| CmdCwagt | 368322 | Comodo 安全解决方案 Inc。 |
| cfrmd | 368320 | Comodo 安全解决方案 Inc。 |
| repdrv | 368310 | 远景解决方案 |
| repmon | 368300 | 远景解决方案 |
| cvofflineFlt32 | 368200 | 量子 Corporation。 |
| cvofflineFlt64 | 368200 | 量子 Corporation。 |
| DsDriver | 368100 | 弯曲磁盘软件 |
| nlcbhelpx86 | 368000 | NetLib |
| nlcbhelpx64 | 368000 | NetLib |
| nlcbhelpi64 | 368000 | NetLib |
| wbfilter | 367950 | 白盒安全性 |
| LRAgentMF | 367900 | LogRhythm Inc。 |
| Drwebfwflt | 367810 | 医生 Web |
| EventMon | 367800 | 医生 Web |
| dsfltfs | 367760 | Digitalsense Co |
| soidriver | 367750 | Sophos Plc |
| drvhookcsmf | 367700 | GrammaTech，Inc。 |
| drvhookcsmf_amd64 | 367700 | GrammaTech，Inc。 |
| avipbb | 367600 | Avira GmbH |
| FileSightMF | 367500 | PA 文件视觉 |
| csaam | 367400 | Cisco 系统 |
| FSMon | 367300 | 1mill |
| filefilter .sys | 367100 | 北京 Zhong 挂起 Jiaxin 计算机技术有限公司。 |
| iiscache | 367000 | Microsoft |
| nowonmf | 366993 | Diskeeper 公司 |
| dktlfsmf | 366992 | Diskeeper 公司 |
| DKDrv | 366991 | Diskeeper 公司 |
| DKRtWrt-XPSP3 的临时修补程序 | 366990 | Diskeeper 公司 |
| HBFSFltr | 366980 | Diskeeper 公司 |
| xoiv8x64 | 366940 | Arcserve |
| xomfcbt8x64 | 366930 | CA |
| KmxAgent | 366920 | CA |
| KmxFile | 366910 | CA |
| KmxSbx | 366900 | CA |
| PointGuardVistaR32 | 366810 | Futuresoft |
| PointGuardVistaR64 | 366810 | Futuresoft |
| PointGuardVistaF | 366800 | Futuresoft |
| PointGuardVista64F | 366800 | Futuresoft |
| vintmfs | 366789 | CondusivTechnologies |
| hiofs | 366782 | Condusiv 技术 |
| intmfs | 366781 | CondusivTechnologies |
| excfs | 366780 | CondusivTechnologies |
| zampit_ml | 366700 | Zampit |
| tesxnginx | 366666 | 腾讯技术 |
| rflog | 366600 | 强制，Inc。 |
| csmon | 366582 | CyberSight Inc。 |
| mumdi | 366540 | ZenmuTech Inc。 |
| LivedriveFilter | 366500 | Livedrive Internet 有限公司 |
| regmonex | 366410 | Tranxition 公司 |
| TXRegMon | 366400 | Tranxition 公司 |
| SDVFilter | 366300 | Soliton Systems K.K。 |
| eLock2FSCTLDriver | 366210 | Egis 技术 Inc。 |
| msiodrv4 | 366200 | Centennial 软件公司 |
| mmPsy32 | 366110 | Resplendence 软件项目 |
| mmPsy64 | 366110 | Resplendence 软件项目 |
| rrMon32 | 366100 | Resplendence 软件项目 |
| rrMon64 | 366100 | Resplendence 软件项目 |
| cvsflt | 366000 | 三月 h Software 有限公司 |
| ktsyncfsflt | 365920 | KnowledgeTree Inc。 |
| nvmon | 365900 | NetVision，Inc。 |
| SnDacs | 365810 | Informzaschita |
| SnExequota | 365800 | Informzaschita |
| llfilter | 365700 | SecureAxis 软件 |
| hafsnk | 365660 | HA Unix Pt |
| DgeDriver | 365655 | Dell Software Inc.。 |
| BWFSDrv | 365650 | 寻找软件 Inc。 |
| CAADFlt | 365601 | 寻找软件 Inc。 |
| QFAPFlt | 365600 | 寻找软件 |
| XendowFLT | 365570 | Credant 技术 |
| fmdrive | 365500 | Cigital，Inc。 |
| EGMinFlt | 365400 | WhiteCell Software Inc。 |
| it2reg | 365315 | Soliton 系统 |
| it2drv | 365310 | Soliton 系统 |
| solitkm | 365300 | Soliton 系统 |
| pgpwdefs | 365270 | Symantec |
| GEProtection | 365260 | Symantec |
| diflt | 365260 | Symantec 公司。 |
| sysMon | 365250 | Symantec |
| ssrfsf | 365210 | Symantec |
| emxdrv2 | 365200 | Symantec |
| reghook | 365150 | Symantec |
| symevnt | 365110 | Symantec |
| spbbcdrv | 365100 | Symantec |
| bhdrvx86 | 365100 | Symantec |
| bhdrvx64 | 365100 | Symantec |
| SISIPSFileFilter | 365010 | Symantec |
| symevent | 365000 | Symantec |
| wrpfv | 364900 | Microsoft |
| UpGuardRealTime | 364810 | UpGuard |
| usbl_ifsfltr | 364800 | SecureAxis |
| ntfsf | 364700 | Sun & 月球上升 |
| BssAudit | 364600 | ByStorm |
| GPMiniFIlter | 364500 | Kalpataru |
| AlfaFF | 364400 | Mg-alfa |
| FSAFilter | 364300 | ScriptLogic |
| GcfFilter | 364200 | GemacmbH |
| FFCFILT.系统 | 364100 | FFC 有限 |
| msnfsflt | 364000 | Microsoft |
| mblmon | 363900 | Packeteer |
| amsfilter | 363800 | Axur 信息 Sec。 |
| rswctrl | 363713 | Douzone Bizon Co |
| mcstrg | 363712 | Douzone Bizon Co |
| fmkkc | 363711 | Douzone Bizon Co |
| nmlhssrv01 | 363710 | Douzone Bizon Co |
| equ8_helper | 363705 | Int3 Software AB |
| strapvista （已停用） | 363700 | AvSoft 技术 |
| SAFE-Agent | 363636 | SAFE-Cyberdefense |
| EstPrmon | 363610 | ESTsoft 公司。 |
| Estprp-64 位 | 363610 | ESTsoft 公司。 |
| EstRegmon | 363600 | ESTsoft 公司。 |
| EstRegp-64 位 | 363600 | ESTsoft 公司。 |
| agfsmon | 363530 | TechnoKom 有限公司。 |
| NlxFF | 363520 | OnGuard Systems LLC |
| 西撒哈拉 | 363511 | Safend |
| 圣 .sys | 363510 | Safend |
| vfdrv | 363500 | Viewfinity |
| topdogfsfilt | 363450 | ManTech |
| xhunter64 | 363400 | Wellbia&#x2024;com |
| uncheater | 363390 | Wellbia&#x2024;com |
| AuditFlt | 363313 | Ionx 解决方案 LLP |
| SPIMiniFilter | 363300 | Software 治愈方法 Inc。 |
| mracdrv | 363230 | 邮件&#x2024;Ru |
| BEDaisy | 363220 | BattlEye 创新 |
| NetAccCtrl | 363200 | 链接 co。 |
| NetAccCtrl64 | 363200 | 链接 co。 |
| hpreg | 363130 | HP |
| qfimdvr | 363120 | Qualys Inc。 |
| QDocumentREF | 363110 | BicDroid Inc。 |
| dsfemon | 363100 | 拓扑公司 |
| AmznMon | 363030 | Amazon Web Services Inc。 |
| iothorfs | 363020 | ioScience |
| ctamflt | 363010 | ComTrade |
| psisolator | 363000 | SharpCrafters |
| QmInspec | 362990 | 北京 QiAnXin 技术。 |
| GagSecurity | 362970 | 北京 Shu Yan 科学 |
| CybKernelTracker | 362960 | CyberArk 软件 |
| filemon | 362950 | Temasoft S.R.L. |
| SCAegis | 362940 | Sogou 有限公司。 |
| fpifp_minifilter | 362930 | ForcePoint LLC。 |
| klifks | 362902 | Kaspersky 等实验室 |
| klifaa | 362901 | Kaspersky 等实验室 |
| Klifsm | 362900 | Kaspersky 等实验室 |
| nxrmflt | 362860 | NextLabs |
| 大型 .sys | 362850 | PolyLogyx LLC |
| AALProtect | 362840 | AlphaAntiLeak |
| egnfsflt | 362830 | Egnyte Inc。 |
| RsFlt | 362820 | Redstor 有限 |
| CentrifyFSF | 362810 | Centrify 公司 |
| Sefo-底部 | 362800 | Solusseum Inc。 |
| SFPMonitor-底部 | 362700 | SonicWall Inc。 |
| minispy-底部 | 361000 | Microsoft |

## <a name="span-id340000_-_349999__fsfilter_undeletespanspan-id340000_-_349999__fsfilter_undeletespanspan-id340000_-_349999__fsfilter_undeletespan340000---349999-fsfilter-undelete"></a><span id="340000_-_349999__FSFilter_Undelete"></span><span id="340000_-_349999__fsfilter_undelete"></span><span id="340000_-_349999__FSFILTER_UNDELETE"></span>340000-349999： FSFilter 取消删除

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| BSSFlt | 346000 | 蓝色鞋软件 LLC |
| ThinIO | 345900 | ThinScale 技术 |
| hmpalert | 345800 | SurfRight |
| nsffkmd64 | 345700 | NetSTAR Inc。 |
| nsffkmd32 | 345700 | NetSTAR Inc。 |
| xbprocfilter | 345600 | Zrxb |
| ifileguard | 345500 | I-O 数据设备，INC。 |
| undelex32 | 345400 | Resplendence 软件项目 |
| undelex64 | 345400 | Resplendence 软件项目 |
| starmon | 345300 | Kantowitz 工程，Inc。 |
| mxRCycle | 345200 | Avanquest |
| UdFilter | 345100 | Diskeeper 公司 |
| it2prtc | 345040 | Soliton Systems K.K。 |
| SolRegFilter | 345030 | Soliton Systems K.K。 |
| SolSecBr | 345020 | Soliton Systems K.K。 |
| SolFCLLi | 345010 | Soliton Systems K.K。 |
| SolFCL | 345000 | Soliton Smart Sec |
| DCVPr | 340700 | SecurStar GmbH |

## <a name="span-id320000_-_329998__fsfilter_anti-virusspanspan-id320000_-_329998__fsfilter_anti-virusspanspan-id320000_-_329998__fsfilter_anti-virusspan320000---329998-fsfilter-anti-virus"></a><span id="320000_-_329998__FSFilter_Anti-Virus"></span><span id="320000_-_329998__fsfilter_anti-virus"></span><span id="320000_-_329998__FSFILTER_ANTI-VIRUS"></span>320000-329998： FSFilter 反病毒

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| zwPxeSvr | 329330 | SecureLink Inc。 |
| zwASatom | 329320 | SecureLink Inc。 |
| wscm | 329310 | Fujitsu 社会科学 |
| IMFFilter | 329300 | IObit 信息技术 |
| CSFlt | 329290 | ConeSecurity Inc。 |
| ospfile_mini | 329230 | OKUMA 公司 |
| SoftFilterxxx | 329222 | WidgetNuri 公司 |
| RansomDefensexxx | 329220 | WidgetNuri 公司 |
| RanPodFS | 329210 | Pooyan 系统 |
| ksfsflt | 329200 | 北京 Kingsoft |
| DeepInsFS | 329190 | 深层 Instinct |
| AppCheckD | 329180 | CheckMAL Inc。 |
| spellmon | 329170 | SpellSecurity |
| WhiteShield | 329160 | Meidensha 公司 |
| reaqtor | 329150 | ReaQta 有限公司。 |
| SE46Filter | 329140 | 技术结点 AB |
| FileScan | 329130 | NPcore 有限公司 |
| ECATDriver | 329120 | 方面 |
| pfkrnl | 329110 | FXSEC 有限公司 |
| epicFilter | 329100 | 隐藏的反射 |
| b9kernel | 329050 | Bit9 Inc。 |
| eeCtrl | 329010 | Symantec |
| 橡皮 .sys （已停用） | 329010 | Symantec |
| SRTSP | 329000 | Symantec |
| SRTSPIT-ia64 系统 | 329000 | Symantec |
| SRTSP64.SYS-x64 系统 | 329000 | Symantec |
| a2ertpx86 | 328920 | 将 emsi Software GmbH |
| a2ertpx64 | 328920 | 将 emsi Software GmbH |
| a2gffx86-x86 | 328910 | 将 emsi Software GmbH |
| a2gffx64-x64 | 328910 | 将 emsi Software GmbH |
| a2gffi64-IA64 | 328910 | 将 emsi Software GmbH |
| a2acc | 328900 | 将 emsi Software GmbH |
| x64 系统上的 a2acc64 | 328900 | 将 emsi Software GmbH |
| FlightRecorder | 328850 | Malwarebytes 公司。 |
| si32_file | 328810 | Scargo Inc。 |
| si64_file | 328810 | Scargo Inc。 |
| mbam | 328800 | Malwarebytes 公司。 |
| EnigmaFileMonDriver | 328770 | EnigmaSoft |
| KUBWKSP | 328750 | Netlor SAS |
| hcp_kernel_acq | 328740 | refractionPOINT |
| SegiraFlt | 328730 | Segira LLC |
| wdocsafe | 328722 | Cheetah Mobile Inc。 |
| lbprotect | 328720 | Cheetah Mobile Inc。 |
| eamonm | 328700 | ESET、spol。 s r.o。 |
| klam | 328650 | Kaspersky 等实验室 |
| MaxProc64 | 328620 | 最大安全软件 |
| MaxProtector | 328610 | 最大安全软件 |
| maxcryptmon | 328601 | 最大安全软件 |
| SDActMon | 328600 | 最大安全软件 |
| fileflt | 328540 | 走向微 Inc。 |
| TmEsFlt | 328530 | 走向微 Inc。 |
| TmEyes | 328520 | 走向微 Inc。 |
| tmevtmgr | 328510 | 走向微 Inc。 |
| tmpreflt | 328500 | 预测 |
| vcMFilter | 328400 | SGRI，有限公司 |
| SAFsFilter | 328300 | Lightspeed Systems Inc。 |
| vsepflt | 328200 | VMware，Inc。 |
| VFileFilter （已重命名） | 328200 | VMware，Inc。 |
| sfavflt | 328130 | Sangfor 技术 |
| sfavflt | 328120 | Sangfor 技术 |
| drivesentryfilterdriver2lite | 328100 | DriveSentry Inc。 |
| WdFilter | 328010 | Microsoft |
| mpFilter | 328000 | Microsoft |
| vrSDetri | 327801 | ETRI |
| vrSDetrix | 327800 | ETRI |
| AhkSvPro | 327720 | Ahkun Co。 |
| AhkUsbFW | 327710 | Ahkun Co。 |
| AhkAMFlt | 327700 | Ahkun Co。 |
| PSINPROC.系统 | 327620 | Panda 安全性 |
| PSINFILE.系统 | 327610 | Panda 安全性 |
| amfsm-Windows XP/2003 x64 | 327600 | Panda 安全性 |
| amm8660-Windows Vista x86 | 327600 | Panda 安全性 |
| amm6460-Windows Vista x64 | 327600 | Panda 安全性 |
| ADSpiderDoc | 327550 | Digitalonnet |
| BkavAutoFlt | 327542 | Bkav 公司 |
| BkavSdFlt | 327540 | Bkav 公司 |
| easyanticheat | 327530 | EasyAntiCheat 解决方案 |
| 5nine | 327520 | 5nine Software Inc。 |
| caavFltr | 327510 | 计算机 Assoc |
| ino_fltr | 327500 | 计算机 Assoc |
| SECOne_USB | 327426 | GRGBanking 设备 |
| SECOne_Proc10 | 327424 | GRGBanking 设备 |
| SECOne_REG10 | 327422 | GRGBanking 设备 |
| SECOne_FileMon10 | 327420 | GRGBanking 设备 |
| WCSDriver | 327410 | 白色 Cloud Security |
| 360qpesv | 327404 | 360软件（北京） |
| dsark | 327402 | Qihoo 360 |
| 360avflt | 327400 | Qihoo 360 |
| scifsflt | 327333 | SECUI 公司 |
| ANVfsm | 327310 | Arcdo |
| CDrRSFlt | 327300 | Arcdo |
| mfdriver | 327250 | Imperva Inc。 |
| EPSMn | 327200 | SGA |
| VTSysFlt | 327150 | 北京金星 |
| TesMon | 327130 | 腾讯 |
| QQSysMonX64 | 327125 | 腾讯 |
| QQSysMon | 327120 | 腾讯 |
| TSysCare | 327110 | Shenzhen 腾讯计算机系统公司有限 |
| TFsFlt | 327100 | Shenzhen 腾讯计算机系统公司有限 |
| avmf | 327000 | Authentium |
| BDFileDefend | 326916 | 百度（北京） |
| BDsdKit | 326914 | 百度 online 网络技术（北京）合作。 |
| bd0003 | 326912 | 百度 online 网络技术（北京）合作。 |
| Bfilter | 326910 | 百度（香港特别行政区）受限 |
| NeoKerbyFilter | 326900 | NeoAutus |
| egnfsflt | 326830 | Egnyte Inc。 |
| RsFlt | 326820 | Redstor 有限 |
| trpmnflt | 326810 | TRAPMINE A.S。 |
| PLGFltr | 326800 | Paretologic |
| WrdWizSecure64 | 326730 | WardWiz |
| wrdwizscanner | 326720 | WardWiz |
| AshAvScan | 326700 | Ashampoo GmbH & |
| Zyfm | 326666 | ZhengYong InfoTech |
| csaav | 326600 | Cisco 系统 |
| oavfm | 326550 | HSM IT 服务 Gmbh |
| SegMD | 326520 | Segurmatica |
| SegMP | 326510 | Segurmatica |
| SegF | 326500 | Segurmatica |
| eeyehv | 326400 | eEye 数字安全 |
| eeyehv64 | 326400 | eEye 数字安全 |
| CpAvFilter | 326311 | CodeProof 技术 Inc。 |
| CpAvKernel | 326310 | CodeProof 技术 Inc。 |
| NovaShield | 326300 | Securitas 技术，Inc。 |
| SheedAntivirusFilterDriver | 326290 | SheedSoft 有限公司 |
| bSyirmf | 326260 | BLACKFORT 安全性 |
| bSysp | 326250 | BLACKFORT 安全性 |
| bSymfdm | 326240 | BLACKFORT 安全性 |
| bSywl | 326235 | BLACKFORT 安全性 |
| bSyrtm | 326230 | BLACKFORT 安全性 |
| bSyaed | 326220 | BLACKFORT 安全性 |
| bSyar | 326210 | BLACKFORT 安全性 |
| BdFileSpy | 326200 | BullGuard |
| npxgd | 326160 | INCA Internet Co。 |
| npxgd64 | 326160 | INCA Internet Co。 |
| tkpl2k | 326150 | INCA Internet Co。 |
| tkpl2k64 | 326150 | INCA Internet Co。 |
| GKFF | 326140 | INCA Internet Co。 |
| GKFF64 | 326140 | INCA Internet Co。 |
| tkdac2k | 326130 | INCA Internet Co。 |
| tkdacxp | 326130 | INCA Internet Co。 |
| tkdacxp64 | 326130 | INCA Internet Co。 |
| tksp2k | 326120 | INCA Internet Co。 |
| tkspxp | 326120 | INCA Internet Co。 |
| tkspxp64 | 326120 | INCA Internet Co。 |
| tkfsft | 326110 | INCA Internet Co，有限公司 |
| tkfsft64-64 位 | 326110 | INCA Internet Co，有限公司 |
| tkfsavxp-32 位 | 326100 | INCA Internet Co，有限公司 |
| tkfsavxp64-64 位 | 326100 | INCA Internet Co，有限公司 |
| SMDrvNt | 326040 | AhnLab，Inc。 |
| ATamptNt | 326030 | AhnLab，Inc。 |
| V3Flt2k | 326020 | AhnLab，Inc。 |
| V3MifiNt | 326010 | Ahnlab |
| V3Ift2k | 326000 | Ahnlab |
| V3IftmNt （旧名称） | 326000 | Ahnlab |
| ArfMonNt | 325990 | Ahnlab |
| AhnRghLh | 325980 | Ahnlab |
| AszFltNt | 325970 | Ahnlab |
| OMFltLh | 325960 | Ahnlab |
| V3Flu2k | 325950 | Ahnlab |
| TfFregNt | 325940 | AhnLab Inc。 |
| AdcVcsNT | 325930 | Ahnlab |
| vcdriv | 325820 | Greatsoft 公司公司 |
| vcreg | 325810 | Greatsoft 公司公司 |
| vchle | 325800 | Greatsoft 公司公司 |
| NxFsMon | 325700 | Novatix 公司 |
| AntiLeakFilter | 325600 | 个人开发人员（Soft3304） |
| NanoAVMF | 325510 | Panda 软件 |
| shldflt | 325500 | Panda 软件 |
| nprosec | 325410 | Norman ASA |
| nregsec | 325400 | Norman ASA |
| issregistry | 325300 | IBM |
| THFilter | 325200 | Sybonic Systems Inc。 |
| pervac | 325100 | PerSystems SA |
| avgmfx86 | 325000 | 平均 Grisoft |
| avgmfx64 | 325000 | 平均 Grisoft |
| avgmfi64 | 325000 | 平均 Grisoft |
| avgmfrs （已停用） | 325000 | 平均 Grisoft |
| FortiAptFilter | 324930 | Fortinet Inc。 |
| fortimon2 | 324920 | Fortinet Inc。 |
| fortirmon | 324910 | Fortinet Inc。 |
| fortishield | 324900 | Fortinet Inc。 |
| mscan-rt | 324800 | SecureBrain 公司 |
| sysdiag | 324600 | Huorong 安全性 |
| agentrtm64 | 324510 | WINS CO。 LTD |
| rswmon | 324500 | WINS CO。 LTD |
| mwfsmfltr | 324420 | MicroWorld Software Services Pvt。 Ltd. |
| gtkdrv | 324410 | GridinSoft LLC |
| GbpKm | 324400 | 气 Tecnologia |
| crnsysm | 324310 | Coranti Inc。 |
| crncache32 | 324300 | Coranti Inc。 |
| crncache64 | 324300 | Coranti Inc。 |
| egambit | 324242 | TEHTRI-安全性 |
| drwebfwft | 324210 | 医生 Web |
| DwShield | 324200 | 医生 Web |
| DwShield64 | 324200 | 医生 Web |
| IProtect | 324150 | EveryZone Inc。 |
| TvFiltr | 324140 | EveryZone INC。 |
| TvDriver | 324130 | EveryZone INC。 |
| TvSPFltr | 324120 | EveryZone INC。 |
| TvPtFile | 324110 | EveryZone INC。 |
| TvMFltr | 324100 | Everyzone |
| SophosED | 324050 | Sophos |
| SAVOnAccess | 324010 | Sophos |
| savonaccess | 324000 | Sophos |
| sld | 323990 | Sophos |
| OADevice | 323900 | 高 Emu |
| pwipf6 | 323800 | PWI，Inc。 |
| EstRkmon | 323700 | ESTsoft 公司。 |
| EstRkr-64 位 | 323700 | ESTsoft 公司。 |
| dwprot | 323610 | 医生 Web |
| Spiderg3 | 323600 | 网络有限公司。 |
| STKrnl64 | 323500 | Verdasys Inc。 |
| UFDFilter | 323400 | Yoggie |
| SCFltr | 323300 | SecurityCoverage，Inc。 |
| fildds | 323200 | Filseclab |
| fsfilter | 323100 | MastedCode 有限公司 |
| fpav_rtp | 323000 | f-保护 |
| cwdriver | 322900 | Leith Bade |
| AYFilter | 322810 | ESTsoft |
| Rtw | 322800 | ESTsoft |
| RSRtw | 322790 | ESTsecurity 公司 |
| RSPCRtw | 322780 | ESTsecurity 公司 |
| HookSys | 322700 | 北京增长的信息技术公司有限 |
| snscore | 322600 | N. & 软件 |
| ssvhook | 322500 | SecuLution GmbH |
| strapvista | 322400 | AvSoft 技术 |
| strapvista64 | 322400 | AvSoft 技术 |
| sascan | 322300 | SecureAge 技术 |
| savant | 322200 | Savant 保护，Inc。 |
| VrARnFlt | 322161 | HAURI |
| VrBBDFlt | 322160 | HAURI |
| vrSDfmx | 322153 | HAURI |
| vrSDfmx | 322152 | HAURI |
| vrSDam | 322151 | HAURI |
| vrSDam | 322150 | HAURI |
| VRAPTFLT | 322140 | HAURI Inc。 |
| VrAptDef | 322130 | HAURI |
| VrSdCore | 322120 | HAURI |
| VrFsFtM | 322110 | HAURI |
| VrFsFtMX （AMD64） | 322110 | HAURI |
| vradfil2 | 322100 | HAURI |
| fsgk | 322000 | f-安全 |
| bouncer | 321950 | CoreTrace 公司 |
| PCTCore64 | 321910 | PC 工具 Pty。 Ltd. |
| PCTCore （旧名称） | 321910 | PC 工具 Pty。 Ltd. |
| ikfilesec | 321900 | PC 工具 Pty。 Ltd. |
| ZxFsFilt | 321800 | 澳大利亚项目 |
| antispyfilter | 321700 | NetMedia Inc。 |
| PZDrvXP | 321600 | VisionPower，有限公司 |
| ggc | 321510 | 快速修复 TechnologiesPvt。 Ltd. |
| catflt | 321500 | 快速修复 TechnologiesPvt。 Ltd. |
| bdsflt | 321490 | 快速修复技术 Pvt。 Ltd. |
| arwflt | 321480 | 快速修复技术 Pvt。 Ltd. |
| csagent | 321410 | CrowdStrike 有限公司。 |
| kmkuflt | 321400 | Komoku Inc。 |
| ntguard | 321337 | IKARUS 安全性 |
| epdrv | 321320 | McAfee Inc。 |
| mfencoas | 321310 | McAfee Inc。 |
| mfehidk | 321300 | McAfee Inc。 |
| swin | 321250 | McAfee Inc。 |
| CyvrFsfd | 321234 | Palo Alto 网络 |
| cmdccav | 321210 | Comodo 组 Inc。 |
| cmdguard | 321200 | Comodo 组 Inc。 |
| K7Sentry | 321100 | K7 计算专用公司。 |
| nsminflt | 321050 | NHN |
| nsminflt64 | 321050 | NHN |
| nvcmflt | 321000 | Norman |
| dgsafe | 320950 | KINGSOFT |
| issfltr | 320900 | ISS |
| hbflt | 320840 | BitDefender SRL |
| bdsvm | 320830 | Bitdefender |
| gzflt | 320820 | BitDefender SRL |
| bddevflt | 320812 | BitDefender SRL |
| ignis | 320811 | BitDefender SRL |
| AVCKF.系统 | 320810 | BitDefender SRL |
| bdfsfltr | 320800 | Softwin |
| bdfm | 320790 | Softwin |
| gemma | 320782 | BitDefender SRL |
| Atc .sys | 320781 | BitDefender SRL |
| AVC3.系统 | 320780 | BitDefender SRL |
| TRUFOS.系统 | 320770 | BitDefender SRL |
| aswmonflt | 320700 | Alwil |
| HookCentre | 320602 | G 数据 |
| PktIcpt | 320601 | G 数据 |
| MiniIcpt | 320600 | G 数据 |
| avgntflt | 320500 | Avira GmbH |
| klam | 320450 | Kaspersky 等实验室 |
| klbg | 320440 | Kaspersky |
| kldback | 320430 | Kaspersky |
| kldlinf | 320420 | Kaspersky |
| kldtool | 320410 | Kaspersky |
| klif | 320401 | Kaspersky 等实验室 |
| klif | 320400 | Kaspersky |
| klam | 320350 | Kaspersky 等实验室 |
| hsmltwhl | 320340 | Hitachi 解决方案 |
| hssfwhl | 320330 | Hitachi 解决方案 |
| DeepInsFS | 320320 | 深层 Instinct 有限公司。 |
| avfsmn | 320310 | Anvisoft |
| lbd | 320300 | Lavasoft AB |
| pavdrv | 320210 | Panzor 网络安全 |
| rvsmon | 320200 | CJSC Returnil 软件 |
| WRKrn | 320110 | Webroot Inc。 |
| ssfmonm | 320100 | Webroot Software，Inc。 |
| vk_fsf | 320050 | AxBx |
| VirtualAgent | 320005 | Symantec |

## <a name="span-id300000_-_309998__fsfilter_replicationspanspan-id300000_-_309998__fsfilter_replicationspanspan-id300000_-_309998__fsfilter_replicationspan300000---309998-fsfilter-replication"></a><span id="300000_-_309998__FSFilter_Replication"></span><span id="300000_-_309998__fsfilter_replication"></span><span id="300000_-_309998__FSFILTER_REPLICATION"></span>300000-309998： FSFilter 复制

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| IntelCAS | 309100 | Intel Corporation |
| mvfs | 309000 | IBM 公司 |
| frxccd | 306000 | FSLogix Inc。 |
| fsrecord | 305000 | Microsoft |
| InstMon | 304201 | Numecent Inc。 |
| StreamingFSD | 304200 | Numecent Inc。 |
| ubcminifilterdriver | 304100 | Ullmore 有限公司。 |
| replistor .sys | 304000 | Esg |
| stfsd | 303900 | 各种技术 |
| xomf | 303800 | CA （XOSOFT） |
| nfid | 303700 | Neverfail 组有限公司 |
| sybfilter | 303600 | Sybase，Inc。 |
| rfsfilter | 303500 | Evidian |
| cvmfsj | 303400 | CommVault Systems，Inc。 |
| iOraFilter | 303300 | Infonic plc |
| bkbmfd32 （x86） | 303200 | BakBone Software，Inc。 |
| bkbmfd64 （x64） | 303200 | BakBone Software，Inc。 |
| mblvn | 303100 | Packeteer |
| AV12NFNT | 303000 | AhnLab |
| mDP_win_mini | 302900 | 宏影响 |
| ctxubs | 302800 | Citrix 系统 Inc。 |
| rrepfsf | 302700 | 玫瑰 Datasystems Inc。 |
| cbfsfilter2017 | 301900 | 超级灵活软件 |
| AxFilter | 301800 | Axcient Inc。 |
| vxfsrep | 301700 | Symantec |
| dellcapfd | 301600 | Dell Inc. |
| Sptres | 301500 | Safend |
| OfficeBackup | 301400 | Ushus 技术 |
| pcvnfilt | 301300 | Blue Coat |
| repdac | 301200 | NSI |
| repkap | 301100 | NSI |
| repdrv | 301000 | NSI |

## <a name="span-id280000_-_289998__fsfilter_continuous_backupspanspan-id280000_-_289998__fsfilter_continuous_backupspanspan-id280000_-_289998__fsfilter_continuous_backupspan280000---289998-fsfilter-continuous-backup"></a><span id="280000_-_289998__FSFilter_Continuous_Backup"></span><span id="280000_-_289998__fsfilter_continuous_backup"></span><span id="280000_-_289998__FSFILTER_CONTINUOUS_BACKUP"></span>280000-289998： FSFilter 连续备份

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klcdp | 288900 | Kaspersky 等实验室 |
| splitinfmon | 288800 | 拆分无限大 |
| versamatic | 288700 | Acertant 技术 |
| Yfilemon | 288690 | Yarisoft |
| ibac | 288600 | Idealstor、LLC。 |
| fkdriver | 288500 | Filekeeper |
| AAFileFilter | 288300 | Dell Inc. |
| hyperoo | 288400 | Hyperoo 有限公司 |
| HyperBacCA | 285000 | 红色入口软件公司 |
| ZMSFsFltr | 284400 | Zenith InfoTech |
| AlfaSC | 284300 | Mg-alfa 公司 |
| hie_ifs | 284200 | Hie 公司 |
| AAFs | 284100 | AppAssure 软件 |
| defilter （旧） | 284000 | Microsoft |
| aFsvDrv | 283100 | ITSTATION Inc。 |
| tilana | 283000 | Tilana Sys |
| VmDPFilter | 282900 | 宏影响 |
| LbFilter | 281700 | Linkverse S.r.l. |
| fbsfd | 281600 | Ferro 软件 |
| dupleemf | 281500 | Duplee SPI，S.L。 |
| file_tracker | 281420 | Acronis Inc。 |
| exbackup | 281410 | Acronis Inc。 |
| afcdp | 281400 | Acronis Inc。 |
| dcefltr | 281300 | Cofio 软件公司 |
| ipmrsync_mfilter | 281200 | OpenMars 企业 |
| cascade. sys | 281100 | 日本软件 |
| filearchive | 281000 | 代码事后 |
| syscdp | 280900 | 系统正常 AB |
| dpnedriver （x86） | 280850 | HP |
| dpnedriver64 （x64） | 280850 | HP |
| hpchgflt | 280800 | HP |
| VirtFile | 280700 | Veritas |
| DeqoCPS | 280600 | Deqo |
| LV_Tracker | 280500 | LiveVault |
| cpbak | 280410 | 检查点软件 |
| tdmonxp | 280400 | TimeData |
| nvfr_cpd | 280310 | Bakbone Software Inc。 |
| nvfr_fdd | 280300 | Bakbone Software Inc。 |
| Sptbkp | 280290 | Safend |
| accessmonitor | 280280 | Briljant Ekonomisystem |

## <a name="span-id260000_-_269998__fsfilter_content_screenerspanspan-id260000_-_269998__fsfilter_content_screenerspanspan-id260000_-_269998__fsfilter_content_screenerspan260000---269998-fsfilter-content-screener"></a><span id="260000_-_269998__FSFilter_Content_Screener"></span><span id="260000_-_269998__fsfilter_content_screener"></span><span id="260000_-_269998__FSFILTER_CONTENT_SCREENER"></span>260000-269998： FSFilter 内容筛选程序

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klshadow | 268300 | Kaspersky 等实验室 |
| TN28 | 268290 | ID 身份验证技术 |
| PGDriver | 268280 | Avecto 有限公司 |
| itseczvdb | 268270 | Innotium Inc。 |
| isarsd | 268260 | ISARS |
| zeoscanner | 268255 | PCKeeper |
| fileHiders | 268250 | PCKeeper |
| cbfltfs4-ObserveIT | 268240 | ObserveIT |
| hipara | 268230 | Allsum LLC |
| AliFileMonitorDriver | 268220 | Alibaba |
| writeGuard | 268210 | TCXA 有限公司。 |
| KKUDKProtectKer | 268200 | Goldmessage 技术合作。 |
| HAWKFIMInt | 268190 | HAWK 网络防御 |
| esaccctl | 268180 | EgoSecure GmbH |
| WSguard | 268170 | 雨刮器 Software UAB |
| Atomizer | 268160 | DragonFlyCodeWorks |
| farwflt | 268150 | Malwarebytes |
| ADSpiderEx2 | 268140 | Digitalonnet |
| sdfilter | 268130 | Igor Zorkov |
| Safe .sys | 268120 | rian@alum.mit.edu |
| mydlpdelete-scanner | 268110 | Medra Teknoloji |
| mydlpscanner | 268100 | Medra Teknoloji |
| hnpro | 268040 | Solupia |
| DLDriverNetMini | 268030 | DeviceLock Inc。 |
| ENFFLTDRV | 268020 | Enforcive 系统 |
| imagentpg | 268012 | Infomaximum |
| crocopg | 268010 | Infomaximum |
| sbapifs | 268000 | Sunbelt 软件 |
| H6kernNT | 267920 | H6N 技术 LLC |
| SGKD32.系统 | 267910 | NetSection 安全性 |
| IccFilter | 267900 | NEC 系统技术 |
| tflbc | 267800 | Tani 电子公司 |
| ArmFlt | 267000 | 防御防病毒 |
| WBDrv | 266700 | Axiana LLC |
| DMSamFilter | 266600 | Digimarc 公司。 |
| mumbl | 266540 | ZenmuTech Inc。 |
| 5nine | 266100 | 5nine Software Inc。 |
| bsfs | 266000 | 快速修复 TechnologiesPvt。 Ltd.  |
| XXRegSFilter | 265910 | Zhe Jiang Xinxin 软件技术。 |
| XXSFilter | 265900 | Zhe Jiang Xinxin 软件技术。 |
| AloahaUSBBlocker | 265800 | Wrocklage Intermedia |
| frxdrv | 265700 | FSLogix Inc。 |
| FolderSecure | 265600 | 最大安全软件 |
| XendowFLTC | 265570 | Credant 技术 |
| RepDac | 265500 | 远景解决方案 |
| tbbdriver | 265400 | Tedesi |
| spcgrd | 265300 | FUJITSU 广泛的解决方案 |
| fdtlock | 265250 | FUJITSU 广泛的解决方案 & 咨询 Inc。 |
| ssfFSC | 265200 | SECUWARE S.L. |
| GagSecurity | 265120 | 北京 Shu Yan 科学 |
| PrintDriver | 265110 | 北京 Shu Yan 科学 |
| activ | 265100 | Rapidware Pty 有限公司 |
| avscan | 265010 | Microsoft |
| sys.databases | 265000 | Microsoft |
| DI_fs | 264910 | Soft-SB |
| wgnpos | 264900 | Orchestria |
| odfltr | 264810 | NetClean 技术 |
| ncpafltr | 264800 | NetClean 技术 |
| ct。 .sys | 264700 | Haute 安全 |
| fvefsmf | 264600 | Fortisphere，Inc。 |
| 块 .sys | 264500 | 自治系统有限 |
| csascr | 264400 | Cisco 系统 |
| SymAFR | 264300 | Symantec 公司 |
| cwnep | 264200 | Websense Inc。 |
| spywareremover | 264150 | C-Netmedia |
| malwarebot | 264140 | C-Netmedia |
| antispywarebot | 264130 | 2Squared Inc。 |
| adwarebot | 264120 | 反间谍软件 LLC |
| 反间谍软件 | 264110 | 反间谍软件 LLC |
| spywarebot | 264100 | C-Netmedia |
| nomp3 | 264000 | Hamish Speirs （私有开发人员） |
| dlfilter | 263900 | Starfield 软件 |
| sifsp | 263800 | 保护孤岛技术有限公司 |
| DLFsFlt | 263700 | CenterTools Software GmbH |
| SamKeng | 263600 | Syvik 有限公司 |
| rml | 263500 | Logis IT 服务 Gmbh |
| vfsmfd | 263410 | Vontu Inc。 |
| vfsmfd | 263400 | Vontu Inc。 |
| acfilter | 263300 | Avalere，Inc。 |
| psecfilter | 263200 | MDI 实验室，Inc。 |
| SolRedirect | 263110 | Soliton 系统 |
| solitkm | 263100 | Soliton 系统 |
| ipcfs | 263000 | NetVeda |
| netgateav_access | 262910 | NETGATE 技术。 s.r.o. |
| spyemrg_access | 262900 | NETGATE 技术。 s.r.o. |
| pxrmcet | 262800 | Proxure Inc。 |
| EgisTecFF | 262700 | Egis 技术 Inc。 |
| fgcpac | 262600 | Fortres 总计公司。 |
| saappctl | 262510 | SecureAge 技术 |
| sadlp | 262500 | SecureAge 技术 |
| CRExecPrev | 262410 | Cybereason |
| PEG2 | 262400 | PE 防护 |
| AdminRunFlt | 262300 | Simon Jarvis |
| wvscr | 262200 | Chengdu Wei Tech Inc。 |
| psepfilter | 262100 | 绝对软件 |
| SAMDriver | 262000 | 峰会 |
| emrcore | 261920 | Ivanti Inc。 |
| wire_fsfilter | 261910 | ThreatSpike 实验室 |
| AMFileSystemFilter | 261900 | AppSense 有限公司 |
| mtflt | 261880 | mTalos Inc。 |
| nxrmflt | 261680 | NextLabs，Inc。 |
| oc_fsfilter | 261300 | Raiffeisen Bank Aval |
| hdlpflt | 261200 | McAfee Inc。 |
| CCFFilter | 261160 | Microsoft |
| cbafilt | 261150 | Microsoft |
| SmbBandwidthLimitFilter | 261110 | Microsoft |
| DfsrRo | 261100 | Microsoft |
| DataScrn | 261000 | Microsoft |
| ldusbro | 260900 | LANDesk Inc。 |
| FileScreenFilter | 260800 | Veritas |
| cpAcOnPnP | 260720 | conpal GmbH |
| cpsgfsmf | 260710 | conpal GmbH |
| psmmfilter | 260700 | PolyServe |
| pctefa | 260650 | PC 工具 Pty。 Ltd. |
| pctefa64 | 260650 | PC 工具 Pty。 Ltd. |
| symefasi | 260610 | Symantec 公司 |
| symefa | 260600 | Symantec |
| symefa64 | 260600 | Symantec |
| aictracedrv_cs | 260500 | AI 咨询 |
| DWFIxxxx | 260410 | SciencePark 公司 |
| DWFIxxxx | 260400 | SciencePark 公司 |
| DSDriver | 260330 | ManageEngine Zoho 公司 |
| mcfltlab | 260320 | 北京 MicroColor |
| FDriver | 260310 | Fox-IT |
| iqpk | 260300 | 保护孤岛技术有限公司 |
| VHDFlt | 260240 | Dell |
| VHDFlt | 260230 | Dell |
| VHDFlt | 260220 | Dell |
| VHDFlt | 260210 | Dell |

## <a name="span-id240000_-_249999__fsfilter_quota_managementspanspan-id240000_-_249999__fsfilter_quota_managementspanspan-id240000_-_249999__fsfilter_quota_managementspan240000---249999-fsfilter-quota-management"></a><span id="240000_-_249999__FSFilter_Quota_Management"></span><span id="240000_-_249999__fsfilter_quota_management"></span><span id="240000_-_249999__FSFILTER_QUOTA_MANAGEMENT"></span>240000-249999： FSFilter 配额管理

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntps_qfs | 245100 | NTP 软件 |
| PSSFsFilter | 245000 | PSS 系统 |
| Sptqmg | 245300 | Safend |
| storqosflt | 244000 | Microsoft |

## <a name="span-id220000_-_229999__fsfilter_system_recoveryspanspan-id220000_-_229999__fsfilter_system_recoveryspanspan-id220000_-_229999__fsfilter_system_recoveryspan220000---229999-fsfilter-system-recovery"></a><span id="220000_-_229999__FSFilter_System_Recovery"></span><span id="220000_-_229999__fsfilter_system_recovery"></span><span id="220000_-_229999__FSFILTER_SYSTEM_RECOVERY"></span>220000-229999： FSFilter 系统恢复

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| file_protector | 227000 | Acronis |
| fbwf | 226000 | Microsoft |
| Klsysrec | 221500 | Kaspersky 等实验室 |
| SFDRV.系统 | 221400 | Utixo LLC |
| sp_prot | 221300 | Xacti 公司 |
| nsfilep | 221200 | Netsupport 有限 |
| syscow | 221100 | 系统正常 AB |
| fsredir | 221000 | Microsoft |

## <a name="span-id200000_-_209999__fsfilter_cluster_file_systemspanspan-id200000_-_209999__fsfilter_cluster_file_systemspanspan-id200000_-_209999__fsfilter_cluster_file_systemspan200000---209999-fsfilter-cluster-file-system"></a><span id="200000_-_209999__FSFilter_Cluster_File_System"></span><span id="200000_-_209999__fsfilter_cluster_file_system"></span><span id="200000_-_209999__FSFILTER_CLUSTER_FILE_SYSTEM"></span>200000-209999： FSFilter 群集文件系统

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CVCBT | 203400 | CommVault Systems，Inc。 |
| ResumeKeyFilter | 202000 | Microsoft |

## <a name="span-id180000_-_189999__fsfilter_hsmspanspan-id180000_-_189999__fsfilter_hsmspanspan-id180000_-_189999__fsfilter_hsmspan180000---189999-fsfilter-hsm"></a><span id="180000_-_189999__FSFilter_HSM"></span><span id="180000_-_189999__fsfilter_hsm"></span><span id="180000_-_189999__FSFILTER_HSM"></span>180000-189999： FSFilter HSM

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcifs | 189900 | Microsoft |
| prjflt | 189800 | Microsoft |
| gameflt | 189750 | Microsoft |
| nvmsqrd | 188900 | NVIDIA 公司 |
| RsFlt | 187000 | Redstor 有限 |
| mnefs | 186800 | Nippon 技术 Lab |
| Svfsf | 186700 | Spharsoft 技术 |
| uVaultFlt | 186650 | 例如 |
| syncmf | 186620 | 氧气云 |
| gwmemory | 186600 | Macrotec LLC |
| cteraflt | 186550 | CTERA 网络有限公司 |
| .dbx .sys | 186500 | Dropbox Inc。 |
| quaddrasi | 186400 | Quaddra 软件 |
| gdrive | 186300 | Google |
| CoreSyncFilter | 186250 | Adobe Systems Inc。 |
| EaseTag | 186200 | EaseVault 技术 Inc。 |
| hcminifilter | 186100 | 祝云公司快乐。 |
| PDFsFilter | 186000 | Raxco Sfotware Inc。 |
| camino | 185900 | CaminoSoft 公司 |
| C2C_AF1R.系统 | 185810 | C2C 系统 |
| DFdriver | 185800 | DataFirst 公司 |
| amfadrv | 185700 | 寻找软件 Inc。 |
| HSMdriver | 185600 | Wim Vervoorn |
| kdfilter | 185555 | Komprise Inc。 |
| htdafd | 185500 | 桥头软 |
| odphflt | 180455 | Microsoft |
| cldflt | 180451 | Microsoft |
| SymHsm | 185400 | Symantec |
| evmf | 185100 | Symantec |
| otfilter | 185000 | Overtone 软 |
| ithsmdrv | 184900 | IBM |
| MfaFilter | 184800 | Waterford 技术 |
| SonyHsmMinifilter | 184700 | 索尼公司 |
| acahsm | 184600 | 自治公司 |
| zlhsm | 184500 | ZL 技术 |
| CFileProtect | 184100 | Zhejiang 安全技术 |
| stc_restore_filter | 184000 | StorageCraft 技术 |
| dvfilter | 183003 | Microsoft |
| Accesstracker | 183002 | Microsoft |
| Changetracker | 183001 | Microsoft |
| Fstier | 183000 | Microsoft |
| hsmcdpflt | 182700 | Metalogix |
| archivmgr | 182690 | Metalogix |
| ntps_oddm | 182600 | NTP 软件 |
| XDFileSys | 182500 | XenData 有限 |
| upmjit | 182400 | Citrix 系统 |
| AtmosFS | 182310 | EMC 公司 |
| DxSpy | 182300 | EMC Software Inc.。 |
| car_hsmflt | 182200 | Caringo，Inc。 |
| BRDriver | 182100 | BitRaider |
| BRDriver64 | 182100 | BitRaider |
| autnhsm | 182000 | 自治公司 |
| cthsmflt | 181970 | ComTrade |
| NxMini | 181900 | NEXSAN |
| neuflt | 181818 | NeuShield |
| npfdaflt | 181800 | Mimosa Systems Inc。 |
| 强制 | 181700 | 强制，Inc。 |
| HPEDpHsmX64 | 181620 | Hewlett-Packard，Co。 |
| HPArcHsmX64 | 181610 | Hewlett-Packard，Co。 |
| hphsmflt | 181600 | Hewlett-Packard，Co。 |
| cparchsm | 181610 | 微聚焦 |
| RepHsm | 181500 | 双重取 Software，Inc。 |
| RepSIS | 181490 | 双重采用软件 |
| SquashCompressionFsFilter | 181410 | Squash 压缩 |
| GXHSM | 181400 | Commvault Systems，Inc。 |
| EdsiHsm | 181300 | 企业数据解决方案，Inc。 |
| BkfMap | 181200 | 数据存储组 |
| hsmfilter | 181100 | GRAU 数据存储 AG |
| mwilcflt | 181020 | Moonwalk 通用 P/L |
| mwilsflt | 181010 | Moonwalk 通用 P/L |
| mwidmflt | 181000 | Moonwalk 通用 P/L |
| HcpAwfs | 181960 | Hitachi 数据系统 |
| sdrefltr | 180950 | Hitachi 数据系统 |
| fltasm | 180900 | 全局360 |
| cnet_hsm | 180850 | Carroll-Net Inc。 |
| pntvolflt | 180800 | 点软件 & 系统 |
| appxstrm | 180710 | Microsoft |
| wimmount | 180700 | Microsoft |
| hsmflt | 180600 | Microsoft |
| dfsrflt | 180500 | Microsoft |
| Storagesyncguard.sys | 180465 | Microsoft |
| Storagesync.sys | 180460 | Microsoft |
| sys.databases | 180450 | Microsoft |
| dfmflt | 180410 | Microsoft |
| sis .sys | 180400 | Microsoft |
| rbt_wfd | 180300 | Riverbed 技术，Inc。 |

## <a name="span-id170000_-_174999__fsfilter_imaging_ex_zipspanspan-id170000_-_174999__fsfilter_imaging_ex_zipspanspan-id170000_-_174999__fsfilter_imaging_ex_zipspan170000---174999-fsfilter-imaging-ex-zip"></a><span id="170000_-_174999__*FSFilter_Imaging_(ex:_.ZIP)"></span><span id="170000_-_174999__*fsfilter_imaging_(ex:_.zip)"></span><span id="170000_-_174999__*FSFILTER_IMAGING_(EX:_.ZIP)"></span>170000-174999： * FSFilter 映像（例如：）。ZIP

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| pfmfs_???。系统 | 172100 | Pismo Technic Inc。 |
| virtual_file | 172000 | Acronis |
| Wimfltr.sys | 170500 | Microsoft |

## <a name="span-id160000_-_169999__fsfilter_compressionspanspan-id160000_-_169999__fsfilter_compressionspanspan-id160000_-_169999__fsfilter_compressionspan160000---169999-fsfilter-compression"></a><span id="160000_-_169999__FSFilter_Compression"></span><span id="160000_-_169999__fsfilter_compression"></span><span id="160000_-_169999__FSFILTER_COMPRESSION"></span>160000-169999： FSFilter 压缩

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CmgFFC | 166000 | Credant 技术 |
| 压缩 .sys | 165000 | Microsoft |
| cmpflt | 162000 | Microsoft |
| IridiumIO | 161700 | Confio |
| logcompressor | 161600 | VelociSQL Inc。 |
| GcfFilter | 161500 | GemacmbH |
| ssddoubler | 161400 | Sinan Karaca |
| Sptcmp | 161300 | Safend |
| wimfsf | 161000 | Microsoft |
| GEFCMP | 160100 | Symantec |

## <a name="span-id140000_-_149999__fsfilter_encryptionspanspan-id140000_-_149999__fsfilter_encryptionspanspan-id140000_-_149999__fsfilter_encryptionspan140000---149999-fsfilter-encryption"></a><span id="140000_-_149999__FSFilter_Encryption"></span><span id="140000_-_149999__fsfilter_encryption"></span><span id="140000_-_149999__FSFILTER_ENCRYPTION"></span>140000-149999： FSFilter 加密

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| FJSeparettiFilterRamMon | 149100 | FUJITSU 有限 |
| psatfilter | 149050 | ProYuga |
| RdFilter | 149040 | CyberEye 调研实验室 |
| gisfile_decryption | 149030 | 中国通信 |
| TIFSFilter | 149020 | SG 公司 |
| OsrDt2 | 149010 | 信息安全公司 |
| EasyKryptMF | 149000 | SoftKrypt LLC |
| 挂锁 | 148910 | IntSoft Inc。 |
| ffecore | 148900 | Winmagic |
| fangcloud | 148860 | 杭州 Yifangyun |
| klvfs | 148810 | Kaspersky 等实验室 |
| Klfle | 148800 | Kaspersky 等实验室 |
| ISFP | 148701 | ALPS 系统集成 |
| ISIRM | 148700 | ALPS 系统 INTEGRATION CO。 |
| ASUSSecDrive | 148650 | ASU |
| ABFilterDriver | 148640 | AlertBoot |
| QDocumentFSF | 148630 | BicDroid Inc。 |
| bfusbenc | 148620 | bitFence Inc。 |
| sztgbfsf | 148610 | SaferZone Co。 |
| mwIPSDFilter | 148600 | Egis 技术 Inc。 |
| csccvdrv | 148500 | 计算机科学公司 |
| aefs | 148400 | Angelltech Corporation Xi'an |
| VTEFsFlt | 148374 | EsComputer 公司 |
| IWCSEFlt | 148300 | InfoWatch |
| GDDmk | 148250 | G 数据软件 AG |
| clcxcore | 148210 | 漂亮解决方案 Inc。 |
| OrisLPDrv | 148200 | CGS 发布技术 |
| nlemsys | 148100 | NETLIB |
| prvflder | 148000 | Microsoft |
| ssefs | 147900 | SecuLution GmbH |
| SePSed | 147800 | Humming 头，Inc。 |
| dlmfencx | 147700 | 数据加密公司 |
| SkyDEnc | 147620 | 天空有限公司 |
| psgcrypt | 147610 | Yokogawa R & L Corp |
| bbfsflt | 147600 | Bloombase |
| qx10efs | 147500 | Quixxant |
| MEfefs | 147400 | Eruces Inc。 |
| medlpflt | 147310 | 检查点软件技术有限公司 |
| dsfa | 147308 | 检查点软件技术有限公司 |
| Snicrpt | 147300 | Systemneeds，Inc。 |
| iCrypt | 147200 | I-O 数据设备，INC。 |
| xdrmflt | 147100 | bluefinsystems |
| dyFsFilter | 147000 | Scrypto 媒体 |
| thinairwin | 146960 | 瘦公司 |
| UcaDataMgr | 146950 | AppSense 有限公司 |
| zesocc | 146900 | Novell |
| mfprom | 146800 | McAfee Inc。 |
| MfeEEFF | 146790 | McAfee Inc。 |
| intefs | 146700 | TianYu 软件 |
| leofs | 146600 | Leotech |
| autocryptater | 146500 | Richard Hagen |
| WavxDMgr | 146400 | Scott Cochrane |
| eedmkxp32 | 146300 | Entrust |
| SbCe | 146200 | SafeBoot |
| iSharedFsFilter | 146100 | Packeteer Inc。 |
| dlrmenc | 146010 | DESlock |
| dlmfenc | 146000 | DESlock |
| aksdf | 145900 | Aladdin 知识系统 |
| DDSFilter | 145800 | WuHan Forworld 软件 |
| SecureShield | 145700 | HMI |
| AifaFE | 145600 | Mg-alfa |
| GBFsMf | 145500 | GreenBorder |
| jmefs | 145400 | 上海 Elec |
| emugufs | 145333 | Emugu 安全 FS |
| VFDriver | 145300 | R 系统 |
| IntelDG | 145250 | Intel Corporation |
| DPMEncrypt | 145240 | Randtronics Pty |
| EVSDecrypt64 | 145230 | Fortium 技术有限公司 |
| skycryptorencfs | 145220 | Onecryptor CJSC. |
| AisLeg | 145210 | 有保障的信息安全 |
| windtalk | 145200 | Hyland 软件 |
| TeamCryptor | 145190 | iTwin Pte。 Ltd. |
| CVDLP | 145180 | CommVault Systems，Inc。 |
| 5nine | 145170 | 5nine Software Inc。 |
| ctpfile | 145160 | 北京 Wondersoft 技术合作。 |
| DPDrv | 145150 | 日本日本 |
| tsdlp | 145140 | Forware |
| KCDriver | 145130 | Tallegra 有限公司 |
| CmgFFE | 145120 | Credant 技术 |
| fgcenc | 145110 | Fortres 总计公司。 |
| sview | 145100 | Cinea |
| TalkeyFilterDriver | 145040 | myTALKEY s.r.o。 |
| FedsFilterDriver | 145010 | 物理光纤公司 |
| stocc | 145000 | Senforce 技术 |
| SnEfs | 144900 | Informzaschita |
| ewSecureDox | 144800 | Echoworx 公司 |
| osrdmk | 144700 | OSR 开放系统资源，Inc。 |
| uldcr | 144600 | NCR 金融解决方案 |
| Tkefsxp-32 位 | 144500 | INCA Internet Co，有限公司 |
| Tkefsxp64-64 位 | 144500 | INCA Internet Co，有限公司 |
| NmlAccf | 144400 | 公司的 NEC 系统技术 |
| SolCrypt | 144300 | Soliton Systems K.K。 |
| IngDmk | 144200 | Ingrian Networks，Inc。 |
| llenc | 144100 | SecureAxis 软件 |
| 由于 securedata | 144030 | SecureAge 技术 |
| lockcube | 144020 | SecureAge 技术 Pte |
| sdmedia | 144010 | SecureAge 技术 |
| mysdrive | 144000 | SecureAge 技术 |
| FileArmor | 143900 | 移动防御 |
| VSTXEncr | 143800 | 通过技术，Inc。 |
| dgdmk | 143700 | Verdasys Inc。 |
| shandy | 143600 | Safend 有限公司。 |
| C2knet | 143520 | Secuware |
| C2kdef | 143510 | Secuware |
| ssfFS | 143500 | SECUWARE S.L. |
| PISRFE | 143400 | Jilin 大学。 |
| bapfecre | 143300 | BitArmor Systems，Inc。 |
| KPSD | 143200 | cihosoft |
| Fcfileio | 143100 | Brainzsquare，有限公司。 |
| cpdrm | 143000 | Pikewerks |
| vmfiltr | 142900 | Vormetric Inc。 |
| VFSEnc | 142811 | Symantec |
| pgpfs | 142810 | Symantec |
| fencry | 142800 | Symantec |
| TmFileEncDmk | 142700 | 走向微 Inc。 |
| cpefs | 142600 | 加密-Pro |
| dekfs | 142500 | KasherLab，有限公司 |
| qlockfilter | 142400 | Binqsoft Inc。 |
| RRFilterDriverStack_d3 | 142300 | 合理保留 |
| cve .sys | 142200 | 绝对软件公司。 |
| spcflt | 142100 | FUJITSU .BSC Inc。 |
| ldsecusb | 142000 | LANDesk Inc。 |
| fencr | 141900 | SODATSW spol. s.r.o. |
| RubiFlt | 141800 | 架式 |
| mfild | 141660 | Penta 安全系统 |
| cbfsfilter2017 | 141635 | 自动机 Inc。 |
| cbfsfilter2017 | 141634 | 自动机 Inc。 |
| cbfsfilter2017 | 141633 | 自动机 Inc。 |
| cbfsfilter2017 | 141632 | 自动机 Inc。 |
| cbfsfilter2017 | 141631 | 自动机 Inc。 |
| cbfsfilter2017 | 141630 | 自动机 Inc。 |
| TypeSquare | 141620 | Morisawa inc。 |
| xbdocfilter | 141610 | Zrxb |
| EVSDecrypt32 | 141600 | Fortium 技术有限公司 |
| EVSDecrypt64 | 141600 | Fortium 技术有限公司 |
| EVSDecryptia64 | 141600 | Fortium 技术有限公司 |
| SophosDt2 | 141510 | Sophos Plc |
| afdriver | 141500 | ATUS 技术 LLC |
| TrivalentFSFltr | 141430 | 网络相关 |
| CmdMnEfs | 141420 | Comodo 安全性 |
| DWENxxxx | 141410 | SciencePark 公司 |
| DWENxxxx | 141400 | SciencePark 公司 |
| hdFileSentryDrv32 | 141300 | Heilig 防卫 |
| hdFileSentryDrv64 | 141300 | Heilig 防卫 |
| CovertxFilter | 141240 | 微聚焦 |
| cplcdt2 | 141230 | conpal GmbH |
| asCryptoFilter | 141220 | 应用的安全 GmbH |
| NetCryptKR | 141210 | NetCrypt Pty 有限公司 |
| BHFilter | 141200 | 用例打下解决方案 |
| Filecrypt | 141100 | Microsoft |
| 加密 .sys | 141010 | Microsoft |
| swapBuffers | 141000 | Microsoft |

## <a name="span-id130000_-_139999__fsfilter_virtualizationspanspan-id130000_-_139999__fsfilter_virtualizationspanspan-id130000_-_139999__fsfilter_virtualizationspan130000---139999-fsfilter-virtualization"></a><span id="130000_-_139999__FSFilter_Virtualization"></span><span id="130000_-_139999__fsfilter_virtualization"></span><span id="130000_-_139999__FSFILTER_VIRTUALIZATION"></span>130000-139999： FSFilter 虚拟化

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klvirt | 138100 | Kaspersky 等实验室 |
| VMagic | 138050 | AI 咨询 |
| GetSAS | 138040 | SAS 研究所 Inc。 |
| rqtNos | 138030 | ReaQta 有限公司。 |
| HIPS64 | 138020 | Recrypt LLC |
| frxdrv | 138010 | FSLogix Inc。 |
| vzdrv | 138000 | Altiris |
| sffsg | 137990 | 海星存储公司 |
| 强制 | 137920 | Symantec 公司 |
| Rasm | 137915 | OpDesk Inc。 |
| boxifier | 137910 | Kenubi |
| xorw | 137900 | CA （XOsoft） |
| ctlua | 137800 | SurfRight B.V. |
| fgccow | 137700 | Fortres 总计公司。 |
| aswSnx | 137600 | ALWIL 软件 |
| AppIsoFltr | 137500 | 内核驱动程序 |
| ptcvfsd | 137400 | PTC |
| BDSandBox | 137300 | BitDefender SRL |
| sxfpss-virt | 137200 | Skanix AS |
| DKRtWrt | 137100 | Diskeeper 公司 |
| ivm | 137000 | RingCube 技术 |
| ivm | 136990 | Citrix 系统 |
| dtiof | 136900 | Instavia Software Inc。 |
| NxTopCP | 136800 | Virtual Ccomputer Inc。 |
| svdriver | 136700 | VMware，Inc。 |
| unifltr | 136600 | Unidesk |
| unidrive （已重命名） | 136600 | Unidesk |
| unirsd | 136600 | Unidesk |
| sys.databases | 136500 | TrendMicro Inc。 |
| odamf | 136450 | 索尼公司 |
| SrMxfMf | 136440 | 索尼公司 |
| pszmf | 136430 | 索尼公司 |
| sxsudfmf | 136410 | 索尼公司 |
| vfammf | 136400 | 索尼公司 |
| VHDFlt | 136240 | Dell |
| VHDFlt | 136230 | Dell |
| VHDFlt | 136220 | Dell |
| VHDFlt | 136210 | Dell |
| ncfsfltr | 136200 | NComputing Inc。 |
| cmdguard | 136100 | COMODO 安全解决方案 Inc。 |
| hpfsredir | 136000 | HP |
| svhdxflt | 135100 | Microsoft |
| luafv | 135000 | Microsoft |
| ivm | 134000 | RingCube 技术 |
| ivm | 133990 | Citrix 系统 |
| frxdrvvt | 132700 | FSLogix Inc。 |
| pfmfs_???。系统 | 132600 | Pismo Technic Inc。 |
| Stcvhdmf | 132600 | StorageCraft 技术公司 |
| appdrv01 | 132500 | 保护技术 |
| virtual_file | 132400 | Acronis |
| pdiFsFilter | 132300 | 最近数据 Inc。 |
| avgvtx86 | 132200 | AVG 技术 CZ |
| avgvtx64 | 132200 | AVG 技术 CZ |
| DataNet_Driver | 132100 | AppSense 有限公司 |
| EgenPage | 132000 | Egenera，Inc。 |
| unidrive-旧 | 131900 | Unidesk |
| ivm | 131800 | RingCube 技术 |
| XiaobaiFsR | 131710 | SHENZHEN UNNOO 有限公司 |
| XiaobaiFs | 131700 | SHENZHEN UNNOO 有限公司 |
| iotfsflt | 131600 | IO，Inc。 |
| mhpvfs | 131500 | Wunix 有限 |
| svdriver | 131400 | SnapVolumes Inc。 |
| Sptvrt | 131300 | Safend |
| antirswf | 131210 | Panzor 网络安全 |
| aicvirt | 131200 | AI 咨询 |
| sfo | 130100 | Microsoft |
| DeVolume | 130000 | Microsoft |

## <a name="span-id120000_-_129999__fsfilter_physical_quota_managementspanspan-id120000_-_129999__fsfilter_physical_quota_managementspanspan-id120000_-_129999__fsfilter_physical_quota_managementspan120000---129999-fsfilter-physical-quota-management"></a><span id="120000_-_129999__FSFilter_Physical_Quota_management"></span><span id="120000_-_129999__fsfilter_physical_quota_management"></span><span id="120000_-_129999__FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>120000-129999： FSFilter 物理配额管理

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| quota | 125000 | Microsoft |
| qafilter | 124000 | Veritas |
| DroboFlt | 123900 | 数据机器人 |

## <a name="span-id100000_-_109999__fsfilter_open_filespanspan-id100000_-_109999__fsfilter_open_filespanspan-id100000_-_109999__fsfilter_open_filespan100000---109999-fsfilter-open-file"></a><span id="100000_-_109999__FSFilter_Open_File"></span><span id="100000_-_109999__fsfilter_open_file"></span><span id="100000_-_109999__FSFILTER_OPEN_FILE"></span>100000-109999： FSFilter 打开文件

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| insyncmf | 105000 | InSync |
| SPILock8 | 100900 | Software 治愈方法 Inc。 |
| Klbackupflt | 100800 | Kaspersky |
| repkap | 100700 | 远景解决方案 |
| symrg | 100600 | Symantec |
| adsfilter | 100500 | PolyServ |

## <a name="span-id80000_-_89999__fsfilter_security_enhancerspanspan-id80000_-_89999__fsfilter_security_enhancerspanspan-id80000_-_89999__fsfilter_security_enhancerspan80000---89999-fsfilter-security-enhancer"></a><span id="80000_-_89999__FSFilter_Security_Enhancer"></span><span id="80000_-_89999__fsfilter_security_enhancer"></span><span id="80000_-_89999__FSFILTER_SECURITY_ENHANCER"></span>80000-89999： FSFilter Security 不得不一直

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| psprotf | 88210 | Panzor 网络安全 |
| DPMACL | 88100 | Randtronics Pty |
| dsbwnck | 88000 | Easy 解决方案 Inc。 |
| cbfsfilter2017 | 87910 | 自动机 |
| cbfsfilter2017 | 87909 | 自动机 Inc。 |
| cbfsfilter2017 | 87908 | 自动机 Inc。 |
| cbfsfilter2017 | 87907 | 自动机 Inc。 |
| cbfsfilter2017 | 87906 | 自动机 Inc。 |
| cbfsfilter2017 | 87905 | 自动机 Inc。 |
| cbfsfilter2017 | 87904 | 自动机 Inc。 |
| cbfsfilter2017 | 87903 | 自动机 Inc。 |
| cbfsfilter2017 | 87902 | 自动机 Inc。 |
| cbfsfilter2017 | 87901 | 自动机 Inc。 |
| cbfsfilter2017 | 87900 | 自动机 Inc。 |
| rsbfsfilter | 87800 | Corel 公司 |
| hsmltflt | 87720 | Hitachi 解决方案 |
| hssfflt | 87710 | Hitachi 解决方案 |
| acmnflt | 87708 | Hitachi 解决方案 |
| ACSKFFD | 87700 | Hitachi 解决方案 |
| MyDLPMF | 87600 | Comodo 组 Inc。 |
| ScuaRaw | 87500 | SCUA Seguran&#231;a da 信息&#231;&#227;o |
| HDSFilter | 87400 | NeoAutus 自动化系统 |
| ikfsmflt | 87300 | IronKey Inc。 |
| Klsec | 87200 | Kaspersky 等实验室 |
| XtimUSBFsFilterDrv | 87190 | Dalian CP-SDT 有限公司 |
| RGFLT_FM | 87180 | Hauri |
| flockflt | 87170 | Ahranta Inc。 |
| ZdCore | 87160 | Zends 技术解决方案 |
| dcrypt | 87150 | ReactOS 基础 |
| hpradeo | 87140 | Pradeo |
| SDFSAGDRV.系统 | 87130 | ALPS 系统 INTEGRATION CO。 |
| SDFSDEVFDRV.系统 | 87120 | ALPS 系统 INTEGRATION CO。 |
| SDIFSFDRV.系统 | 87110 | ALPS 系统 INTEGRATION CO。 |
| SDFSFDRV.系统 | 87100 | ALPS 系统 INTEGRATION CO。 |
| CModule | 87070 | Zhejiang 安全技术 |
| HHRRPH | 87010 | H + H Software GmbH |
| HHVolFltr | 87000 | H + H Software GmbH |
| SbieDrv | 86900 | Sandboxie。 D |
| assetpro | 86800 | pyaprotect&#x2024;com |
| dlp .sys | 86700 | Tellus 软件 |
| eps | 86600 | Lumension 安全性 |
| RapportPG64 | 86500 | Trusteer |
| amminifilter | 86400 | AppSense |
| Sniflt | 86300 | Systemneeds，Inc。 |
| SecFile | 86200 | 由设计 Inc. 保护。 |
| philly | 86110 | triCerat Inc。 |
| reggy | 86100 | triCerat Inc。 |
| cygfilt | 86000 | Livegrid 合并 |
| sys.databases | 85900 | D3L |
| csareg | 85810 | Cisco 系统 |
| csaenh | 85800 | Cisco 系统 |
| asEpsDrv | 85750 | ASHINI |
| CIDACL | 85700 | GE 航空（数字式 Systems Germantown） |
| CVDLP | 85610 | CommVault Systems，Inc。 |
| QGPEFlt | 85600 | 寻找软件 |
| Drveng | 85500 | CA |
| vracfil2 | 85400 | HAURI |
| TFsDisk | 85300 | Teruten |
| rcMiniDrv | 85200 | REDGATE，有限公司 |
| SnMc5xx | 85100 | Informzaschita |
| FSPFltd | 85010 | Mg-alfa |
| AifaFFP | 85000 | Mg-alfa |
| EsAccCtlFE | 84901 | EgoSecure GmbH |
| DpAccCtl | 84900 | Softbroker GmbH |
| privman | 84800 | BeyondTrust |
| eumntvol | 84700 | Eugrid Inc。 |
| SoloEncFilter | 84600 | Soliton 系统 |
| sbfilter | 84500 | UC4 软件 |
| cposfw | 84450 | 检查点软件技术有限公司 |
| vsdatant | 84400 | 区域实验室 LLC |
| SePnet | 84350 | Humming 头，Inc。 |
| SePuld | 84340 | Humming 头，Inc。 |
| SePpld | 84330 | Humming 头，Inc。 |
| SePfsd | 84320 | Humming 头，Inc。 |
| SePwld | 84310 | Humming 头，Inc。 |
| SePprd | 84300 | Humming 头，Inc。 |
| InPFlter | 84200 | Humming 头，Inc。 |
| CProCtrl | 84100 | 加密-Pro |
| spyshelter | 84000 | Datpol |
| clpinspprot | 83900 | 信息技术公司公司有限公司。 |
| uvmfsflt | 83376 | NEC 公司  |
| ProtectIt | 82373 | Tb 公司 |
| dguard | 82300 | Dmitry Varshavsky |
| NSUSBStorageFilter | 82200 | NetSupport 有限公司 |
| RMSEFFMV.系统 | 82100 | CJSC Returnil 软件 |
| BoksFLAC | 82000 | Fox 技术 |
| cpAcOnPnP | 81910 | conpal GmbH |
| cpsgfsmf | 81900 | conpal GmbH |
| ndevsec | 81800 | Norman ASA |
| ViewIntus_RTDG | 81700 | Pentego 技术有限公司 |
| 代表太空飞船 | 81630 | 代表太空飞船数字 Pty 有限公司 |
| zam | 81620 |  |
| ANXfsm | 81610 | Arcdo |
| CDrSDFlt | 81600 | Arcdo |
| crnselfdefence32 | 81500 | Coranti Inc。 |
| crnselfdefence64 | 81500 | Coranti Inc。 |
| zlock_drv | 81400 | SecurIT |
| f101fs | 81300 | Fortres 总计公司。 |
| sysgar | 81200 | 核心数据恢复 |
| EmbargoM | 81100 | ScriptLogic |
| ngssdef | 81050 | Wontok Inc。 |
| ssb | 81041 | Wontok Inc。 |
| regflt | 81040 | Wontok Inc。 |
| fsds2a | 81000 | Splitstreem 有限公司 |
| csacentr | 80900 | Cisco 系统 |
| ScvFLT50 | 80850 | Secuve 有限公司 |
| paritydriver | 80800 | Bit9，Inc。 |
| nkfsprot | 80710 | Konneka |
| nkprot | 80700 | KONNEKA 信息技术 |
| acpadlock | 80691 | IntSoft Co |
| ksmf | 80690 | IntSoft Co |
| sys.databases | 80680 | CrowdStrike |
| SophosED | 80670 | Sophos |
| jazzfile | 80660 | 爵士乐网络 |
| SMXFs | 80500 | OSR |

## <a name="span-id60000_-_69999__fsfilter_copy_protectionspanspan-id60000_-_69999__fsfilter_copy_protectionspanspan-id60000_-_69999__fsfilter_copy_protectionspan60000---69999-fsfilter-copy-protection"></a><span id="60000_-_69999__FSFilter_Copy_Protection"></span><span id="60000_-_69999__fsfilter_copy_protection"></span><span id="60000_-_69999__FSFILTER_COPY_PROTECTION"></span>60000-69999： FSFilter Copy 保护

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| d3clock | 67000 | D3CRYPT3D LLC |
| cbfltfs4 | 66500 | I3D 技术 Inc。 |
| CkProcess | 66100 | KASHU 系统设计 INC。 |
| dlmfprot | 66000 | 数据加密 Sys |
| baprtsef | 65700 | BitArmor Systems，Inc。 |
| sxfpss | 65600 | Skanix AS |
| rgasdev | 65500 | Macrovision |
| SkyFPDrv | 65410 | 天空有限公司。 |
| SkyLWP | 65400 | 天空有限公司。 |
| SnEraser | 65300 | Informzaschita |
| vfilter | 65200 | RSJ Software GmbH |
| COGOFlt32 | 65100 | Fortium 技术有限公司 |
| COGOFlt64 | 65100 | Fortium 技术有限公司 |
| COGOFLTia64 | 65100 | Fortium 技术有限公司 |
| 清理器 | 65000 | Microsoft |
| BRDriver | 64000 | BitRaider LLC |
| BRDriver64 | 64000 | BitRaider LLC |
| X7Ex | 62500 | Exent 技术有限公司 |
| LibertyFSF | 62300 | Bayalink 解决方案 Co |
| axfsdrv2 | 62100 | Axence Software Inc。 |
| sds | 62000 | 出口软件 |
| TotalSystemAuditor | 61600 | ANRC LLC |
| MBAMApiary | 61500 | Malwarebytes 公司。 |
| WA_FSW | 61400 | Programas Administraci&#243;n y Mejoramiento |
| ViewIntus_RTAS | 61300 | Pentego 技术 |
| tffac | 61200 | Toshiba 公司 |
| tccp | 61100 | TrusCont 有限公司 |
| KomFS | 61000 | KOM 网络 |

## <a name="span-id40000_-_49999__fsfilter_bottomspanspan-id40000_-_49999__fsfilter_bottomspanspan-id40000_-_49999__fsfilter_bottomspan40000---49999-fsfilter-bottom"></a><span id="40000_-_49999__FSFilter_Bottom"></span><span id="40000_-_49999__fsfilter_bottom"></span><span id="40000_-_49999__FSFILTER_BOTTOM"></span>40000-49999： FSFilter 底端

| 微                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| RMPFileMounter | 48000 | ManageEngine Zoho |
| cbfsfilter2017 | 47400 | 12-12 协同 |
| pfmfs_???。系统 | 47300 | Pismo Technic Inc。 |
| DLDriverMiniFlt | 47200 | DeviceLock Inc。 |
| hsmltlib | 47110 | Hitachi 解决方案 |
| hskdlib | 47100 | Hitachi 解决方案 |
| acmnlib | 47090 | Hitachi 解决方案 |
| aictracedrv_b | 47000 | AI 咨询 |
| hhdcfltr | 46900 | Seagate 技术 |
| Npsvctrig | 46000 | Microsoft |
| klvfs | 44900 | Kaspersky 等实验室 |
| Klbackupflt | 44890 | Kaspersky 等实验室 |
| rsfxdrv | 41000 | Microsoft |
| defilter | 40900 | Microsoft |
| AppVVemgr | 40800 | Microsoft |
| wofadk | 40730 | Microsoft |
| wof | 40700 | Microsoft |
| fileinfo | 40500 | Microsoft |
| WinSetupBoot | 40400 | Microsoft |

## <a name="span-id20000_-_29999__fsfilter_systemspanspan-id20000_-_29999__fsfilter_systemspanspan-id20000_-_29999__fsfilter_systemspan20000---29999-fsfilter-system"></a><span id="20000_-_29999__FSFilter_System"></span><span id="20000_-_29999__fsfilter_system"></span><span id="20000_-_29999__FSFILTER_SYSTEM"></span>20000-29999： FSFilter 系统

无。
