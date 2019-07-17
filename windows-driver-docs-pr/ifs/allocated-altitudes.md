---
title: 分配的等级
description: 分配的等级
ms.assetid: EC1993FB-5219-4C0C-A76A-05937A461C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b132c97b0e17b76b2b2d9d561dcc5cad6748cee9
ms.sourcegitcommit: d4ade685d5401960be55f9b44861547fbd222d35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68246947"
---
# <a name="allocated-altitudes"></a>分配的等级

文件系统微筛选器驱动程序开发到筛选器管理器模型必须具有名为海拔高度，用于定义其位置相对于存在于文件系统堆栈中其他微筛选器的唯一标识符。 由 Microsoft 根据微筛选器要求和加载顺序组分配海拔微筛选器的地区。

若要请求微筛选器海拔高度多，请参阅[微筛选器海拔高度请求](minifilter-altitude-request.md)。

为每个以下的加载顺序组下面列出了当前的海拔高度分配。

## <a name="span-id420000-429999filterspanspan-id420000-429999filterspanspan-id420000-429999filterspan420000---429999-filter"></a><span id="420000_-_429999__Filter"></span><span id="420000_-_429999__filter"></span><span id="420000_-_429999__FILTER"></span>420000-429999:Filter

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| ntoskrnl.exe | 425500 | Microsoft |
| ntoskrnl.exe | 425000 | Microsoft |

## <a name="span-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspan400000---409999-fsfilter-top"></a><span id="400000_-_409999__FSFilter_Top"></span><span id="400000_-_409999__fsfilter_top"></span><span id="400000_-_409999__FSFILTER_TOP"></span>400000-409999:FSFilter 顶部

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| wcnfs.sys | 409900 | Microsoft |
| bindflt.sys | 409800 | Microsoft |
| cldflt.sys | 409500 | Microsoft |
| iorate.sys | 409010 | Microsoft |
| ioqos.sys | 409000 | Microsoft |
| fsdepends.sys | 407000 | Microsoft |
| sftredir.sys | 406000 | Microsoft |
| dfs.sys | 405000 | Microsoft |
| tracker.sys | 404910 | Acronis |
| csvnsflt.sys | 404900 | Microsoft |
| csvflt.sys | 404800 | Microsoft |
| Microsoft.Uev.AgentDriver.sys | 404710 | Microsoft |
| AppvVfs.sys | 404700 | Microsoft |
| CCFFilter.sys | 404600 | Microsoft |
| dciogrd.sys | 402010 | Datacloak 技术 |
| Dewdrv.sys | 402000 | Dell 技术 |
| zsusbstorfilt.sys | 401910 | Zshield Inc |
| eaw.sys | 401900 | Raytheon 网络解决方案 |
| TVFsfilter.sys | 401800 | TrustView |
| KKDiskProtecter.sys | 401700 | Goldmsg |
| AgentComm.sys | 401600 | 开发控股 Inc |
| rvsavd.sys | 401500 | CJSC Returnil 软件 |
| DGMinFlt.sys | 401410 | 数字保护者 inc.保留所有权利。 |
| dgdmk.sys | 401400 | Verdasys inc.保留所有权利。 |
| tusbstorfilt.sys | 401300 | SimplyCore LLC |
| pcgenfam.sys | 401200 | Soluto |
| atrsdfw.sys | 401100 | Altiris |
| tpfilter.sys | 401000 | RedPhone 安全 |
| MBIG2Prot.sys | 400920 | Malwarebytes Inc |
| mbamwatchdog.sys | 400900 | Malwarebytes Corporation |
| DSESafeCtrlDrv.sys | 400803 | 上海 Eff 软 IT |
| edevmon.sys | 400800 | 重置 spol。 s r.o. |
| vmwflstor.sys | 400700 | VMware，inc. |
| TsQBDrv.sys | 400600 | 腾讯技术 |
| WRAEKernel.sys | 400500 | Webroot inc.保留所有权利。 |

## <a name="span-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspan360000---389999-fsfilter-activity-monitor"></a><span id="360000_-_389999__FSFilter_Activity_Monitor"></span><span id="360000_-_389999__fsfilter_activity_monitor"></span><span id="360000_-_389999__FSFILTER_ACTIVITY_MONITOR"></span>360000-389999:FSFilter 活动监视器

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| klboot.sys | 389510 | Kaspersky 实验室 |
| klfdefsf.sys | 389500 | Kaspersky 实验室 |
| CBFSFilter2017.sys | 389250 | SecureLink inc.保留所有权利。 |
| NWEDriver.sys | 389240 | Dell 技术 |
| cytmon.sys | 389230 | Cytrence Inc |
| SophosED.sys | 389220 | Sophos |
| MonsterK.sys | 389210 | Somma Inc |
| IFS64.sys | 389200 | Ashampoo 开发 |
| TSTFilter.sys | 389190 | ThinScale 技术 |
| VrnsFilter.sys | 389180 | Varonis Ltd |
| lrtp.sys | 389170 | Lenovo 北京 |
| ipcomfltr.sys | 389160 | Bluzen Inc |
| SvCBT.sys | 389150 | Spharsoft 技术 |
| mbamshuriken.sys | 389140 | Malwarebytes |
| ContainerMonitor.sys | 389130 | 浅绿色安全 |
| SaMFlt.sys | 389120 | DreamCrafts |
| RuiMinispy.sys | 389117 | RuiGuard Ltd |
| RuiFileAccess.sys | 389115 | RuiGuard Ltd |
| RuiEye.sys | 389113 | RuiGuard Ltd |
| RuiMachine.sys | 389111 | RuiGuard Ltd |
| windd.sys | 389110 | Comae 技术 |
| cbfsfilter2017.sys | 389105 | Basein 网络 |
| taobserveflt.sys | 389100 | ThinAir 实验室 Inc |
| vollock.sys | 389092 | Man 技术 Inc |
| drbdlock.sys | 389090 | Man 技术 Inc |
| dcfsgrd.sys | 389085 | Datacloak 技术 |
| hsmltmon.sys | 389080 | 人： Hitachi Solutions |
| AternityRegistryHook.sys | 389070 | Aternity Ltd |
| MozyNextFilter.sys | 389068 | Carbonite Inc |
| MozyCorpFilter.sys | 389067 | Carbonite Inc |
| MozyEntFilter.sys | 389066 | Carbonite Inc |
| MozyOEMFilter.sys | 389065 | Carbonite Inc |
| MozyEnterpriseFilter.sys | 389064 | Carbonite Inc |
| MozyProFilter.sys | 389063 | Carbonite Inc |
| MozyHomeFilter.sys | 389062 | Carbonite Inc |
| BDSFilter.sys | 389061 | Carbonite Inc |
| CSBFilter.sys | 389060 | Carbonite Inc |
| ChemometecFilter.sys | 389050 | ChemoMetec |
| SentinelMonitor.sys | 389040 | SentinelOne |
| DhWatchdog.sys | 389030 | Microsoft |
| edrsensor.sys | 389025 | Bitdefender SRL |
| bdprivmon.sys | 389022 | Bitdefender SRL |
| NpEtw.sys | 389020 | Koby Kahane |
| OczMiniFilter.sys | 389010 | OCZ 存储 |
| ielcp.sys | 389004 | Intel Corporation |
| IESlp.sys | 389002 | Intel Corporation |
| IntelCAS.sys | 389000 | Intel Corporation |
| boxifier.sys | 388990 | Kenubi |
| SamsungRapidFSFltr.sys | 388980 | NVELO inc.保留所有权利。 |
| drsfile.sys | 388970 | MRY inc.保留所有权利。 |
| CbFltFs4.sys | 388966 | Simopro 技术 |
| CrUnCopy.sys | 388964 | 深圳 CloudRiver |
| aictracedrv_am.sys | 388960 | AI 咨询 |
| fiopolicyfilter.sys | 388954 | SanDisk inc.保留所有权利。 |
| fcontrol.sys | 388950 | SODATSW spol。 s r.o. |
| qfilter.sys | 388940 | 仲裁实验室 |
| Redlight.sys | 388930 | Trustware Ltd |
| eps.sys | 388920 | Lumension |
| VHDTrack.sys | 388915 | Intronis Inc |
| VHDDelta.sys | 388912 | Niriva LLC |
| FSTrace.sys | 388910 | Niriva LLC |
| YahooStorage.sys | 388900 | Yahoo 日本 Corporation |
| KeWF.sys | 388890 | KEBA AG |
| epregflt.sys | 388888 | 检查点软件 |
| epklib.sys | 388886 | 检查点软件 |
| zsfprt.sys | 388880 | k4solution Co. |
| dsflt.sys | 388876 | cEncrypt |
| bfaccess.sys | 388872 | bitFence inc.保留所有权利。 |
| xcpl.sys | 388870 | X 云系统 |
| DCFAFilter.sys | 388866 | ManageEngine Zoho |
| RMPHVMonitor.sys | 388865 | ManageEngine Zoho |
| FAPMonitor.sys | 388864 | ManageEngine Zoho |
| EaseFlt.sys | 388860 | EaseVault Technologies inc. |
| rpwatcher.sys | 388855 | 最佳的安全性 |
| sieflt.sys | 388852 | 快速修复技术 Pvt。 Ltd. |
| cssdlp.sys | 388851 | 快速修复技术 Pvt。 Ltd. |
| cssdlp.sys | 388850 | CoSoSys |
| INISBDrv64.sys | 388840 | Initech inc.保留所有权利。 |
| trace.sys | 388831 | Fitsec Ltd |
| SandDriver.sys | 388830 | Fitsec Ltd |
| dskmn.sys | 388820 | Honeycomb 技术 |
| xkfsfd.sys | 388810 | Jiransoft Co.，Ltd |
| pcpifd.sys | 388800 | Jiransoft Co.，Ltd |
| NNTInfo.sys | 388790 | 新的 Net 技术限制 |
| FsMonitor.sys | 388780 | IBM |
| CVCBT.sys | 388770 | CommVault Systems，inc.保留所有权利。 |
| AwareCore.sys | 388760 | TaaSera inc.保留所有权利。 |
| laFS.sys | 388750 | NetworkProfi ltd. |
| fsnk.sys | 388740 | SoftPerfect 研究 |
| RGNT.sys | 388730 | HFN inc.保留所有权利。 |
| fltRs329.sys | 388720 | 受保护的全球 inc.保留所有权利。 |
| ospmon.sys | 388710 | SC ODEKIN 解决方案 SRL |
| edsigk.sys | 388700 | 企业数据的解决方案，inc. |
| fiometer.sys | 388692 | 合成 io |
| dcSnapRestore.sys | 388690 | 合成 io |
| fam.sys | 388680 | 快速修复技术 Pvt。 Ltd. |
| vidderfs.sys | 388675 | Vidder inc.保留所有权利。 |
| Tritiumfltr.sys | 388670 | Tritium inc.保留所有权利。 |
| HexisFSMonitor.sys | 388660 | Hexis 网络解决方案 |
| BlackbirdFSA.sys | 388650 | BeyondTrust inc.保留所有权利。 |
| TMUMS.sys | 388642 | Trend Micro inc.保留所有权利。 |
| hfileflt.sys | 388640 | Trend Micro inc.保留所有权利。 |
| TMUMH.sys | 388630 | Trend Micro inc.保留所有权利。 |
| AcDriver.sys | 388620 | Trend Micro，inc. |
| SakFile.sys | 388610 | Trend Micro，inc. |
| SakMFile.sys | 388600 | Trend Micro，inc. |
| rsfdrv.sys | 388580 | Clonix Co |
| alcapture.sys | 388570 | 太空飞船数字 Pty Ltd |
| kmNWCH.sys | 388560 | IGLOO SECURITY，inc |
| ISIRMFmon.sys | 388550 | 安装 ALPS 系统集成 CO。 |
| EsProbe.sys | 388542 | Stormshield |
| heimdall.sys | 388540 | Arkoon 网络安全 |
| thetta.sys | 388532 | Syncopate |
| thetta.sys | 388531 | Syncopate |
| thetta.sys | 388530 | Syncopate |
| DTPL.sys | 388520 | 连接 SHIFT LTD |
| CyOptics.sys | 388514 | Cylance inc.保留所有权利。 |
| CyProtectDrv32.sys | 388510 | Cylance inc.保留所有权利。 |
| CyProtectDrv64.sys | 388510 | Cylance inc.保留所有权利。 |
| tbfsfilt.sys | 388500 | 第三个队列 |
| IvAppMon.sys | 388491 | Ivanti |
| LDSecDrv.sys | 388490 | LANDESK 软件 |
| SGResFlt.sys | 388480 | Samsung SDS Ltd |
| CwMem2k64.sys | 388470 | ApSoft |
| axfltdrv.sys | 388460 | Axact Pvt Ltd |
| RMDiskMon.sys | 388450 | Qingdao Ruanmei 网络技术 Co. |
| diskactmon.sys | 388440 | Qingdao Ruanmei 网络技术 Co. |
| Codex.sys | 388430 | GameHi Co. |
| CatMF.sys | 388420 | Logichron Inc |
| RW7FsFlt.sys | 388410 | PJSC KP VTI |
| aswSP.sys | 388401 | Avast 软件 |
| aswFsBlk.sys | 388400 | ALWIL 软件 |
| ThreatStackFIM.sys | 388380 | 威胁堆栈 |
| BOsCmFlt.sys | 388370 | Barkly 保护 inc.保留所有权利。 |
| BOsFsFltr.sys | 388370 | Barkly 保护 inc.保留所有权利。 |
| FeKern.sys | 388360 | FireEye inc.保留所有权利。 |
| libwamf.sys | 388350 | OPSWAT inc.保留所有权利。 |
| SZEDRDrv.sys | 388346 | SaferZone Co. |
| szardrv.sys | 388345 | SaferZone Co. |
| szpcmdrv.sys | 388341 | SaferZone Co. |
| szdfmdrv.sys | 388340 | SaferZone Co. |
| szdfmdrv_usb.sys | 388331 | SaferZone Co. |
| sprtdrv.sys | 388330 | SaferZone Co. |
| SWFsFltrv2.sys | 388321 | Solarwinds LLC |
| SWFsFltr.sys | 388320 | Solarwinds LLC |
| flashaccelfs.sys | 388310 | 网络设备 |
| changelog.sys | 388300 | 网络设备 |
| stcvsm.sys | 388250 | StorageCraft 技术 |
| aUpDrv.sys | 388240 | ITSTATION Inc |
| fshs.sys | 388222 | F 安全 |
| fshs.sys | 388221 | F 安全 |
| fsatp.sys | 388220 | F 安全 |
| SecdoDriver.sys | 388210 | Secdo |
| TGFSMF.sys | 388200 | Tetraglyph 技术 |
| evscase.sys | 388100 | 年 3 月一起共享软件 Ltd |
| VSScanner.sys | 388050 | VoodooSoft |
| HDRansomOffDrv.sys | 388044 | Heilig 防御 LLC |
| HDCorrelateFDrv.sys | 388042 | Heilig 防御 LLC |
| HDFileMon.sys | 388040 | Heilig 防御 LLC |
| tsifilemon.sys | 388012 | 对讲机 inc.保留所有权利。 |
| MarSpy.sys | 388010 | 对讲机 inc.保留所有权利。 |
| AGSysLock.sys | 388002 | AppGuard LLC |
| AGSecLock.sys | 388001 | AppGuard LLC |
| BrnFileLock.sys | 388000 | 蓝色凸缘网络 |
| BrnSecLock.sys | 387990 | 蓝色凸缘网络 |
| LCmPrintMon.sys | 387978 | YATEM 有限公司 |
| LCgAdMon.sys | 387977 | YATEM 有限公司 |
| LCmAdMon.sys | 387976 | YATEM 有限公司 |
| LCgFileMon.sys | 387975 | YATEM 有限公司 |
| LCmFile.sys | 387974 | YATEM 有限公司 |
| LCgFile.sys | 387972 | YATEM 有限公司 |
| LCmFileMon.sys | 387970 | YATEM 有限公司 |
| IridiumSwitch.sys | 387960 | Confio |
| scensemon.sys | 387950 | AppiXoft |
| ruaff.sys | 387940 | RUNEXY |
| bbfilter.sys | 387930 | derivo GmbH |
| Bfmon.sys | 387920 | 有限的百度 （中国香港特别行政区） |
| bdsysmon.sys | 387912 | 百度联机网络 |
| BdRdFolder.sys | 387910 | 百度 （北京） |
| mlsaff.sys | 387901 | RUNEXY |
| pscff.sys | 387900 | Weing Co.，Ltd. |
| fcnotify.sys | 387880 | TCXA ltd. |
| aaf.sys | 387860 | Actifio Inc |
| gddcv.sys | 387840 | G 数据 Software AG |
| wgfile.sys | 387820 | 橙色 WERKS Inc |
| zesfsmf.sys | 387800 | Novell |
| uamflt.sys | 387700 | Sevtechnotrans |
| ehdrv.sys | 387600 | 重置，spol。 s r.o. |
| DattoFSF.sys | 387560 | Datto Inc |
| FileSystemCBT.sys | 387550 | Rubrik Inc |
| Snilog.sys | 387500 | Systemneeds，Inc |
| tss.sys | 387400 | Tiversa Inc |
| LmDriver.sys | 387390 | 在软 Kft。 |
| WDCFilter.sys | 387330 | Interset inc.保留所有权利。 |
| altcbt.sys | 387320 | Altaro ltd. |
| bapfecpt.sys | 387310 | BitArmor 系统，Inc |
| bamfltr.sys | 387300 | BitArmor 系统，Inc |
| TrustedEdgeFfd.sys | 387200 | FileTek，inc. |
| MRxGoogle.sys | 387100 | Google，inc. |
| YFSDR。SYS | 387010 | Yokogawa R & L Corp |
| YFSD。SYS | 387000 | Yokogawa R & L Corp |
| YFSRD.sys | 386990 | Yokogawa R & L Corp |
| psgfoctrl.sys | 386990 | Yokogawa R & L Corp |
| psgdflt.sys | 386980 | Yokogawa R & L Corp |
| USBPDH。SYS | 386901 | 高级计算开发中心 |
| pecfilter.sys | 386900 | C DAC 海得拉巴 |
| GKPFCB.sys | 386810 | INCA Internet Co. |
| GKPFCB64.sys | 386810 | INCA Internet Co. |
| 在 32 位 TkPcFtCb.sys | 386800 | INCA Internet Co.，Ltd. |
| 64 位上的 TkPcFtCb64.sys | 386800 | INCA Internet Co.，Ltd. |
| bmregdrv.sys | 386731 | Yandex LLC |
| bmfsdrv.sys | 386730 | Yandex LLC |
| CarbonBlackK.sys | 386720 | Bit9 inc.保留所有权利。 |
| ScAuthFSFlt.sys | 386710 | LLC 的安全代码 |
| ScAuthIoDrv.sys | 386700 | LLC 的安全代码 |
| mfeaskm.sys | 386610 | McAfee inc.保留所有权利。 |
| mfencfilter.sys | 386600 | McAfee |
| WinFLAHdrv.sys | 386540 | NewSoftwares&#x2024;net，inc. |
| WinFLAdrv.sys | 386530 | NewSoftwares&#x2024;net，inc. |
| WinDBdrv.sys | 386520 | NewSoftwares&#x2024;net，inc. |
| WinFLdrv.sys | 386510 | NewSoftwares&#x2024;net，inc. |
| WinFPdrv.sys | 386500 | NewSoftwares&#x2024;net，inc. |
| SkyWPDrv.sys | 386435 | 天空 Co.，Ltd. |
| SkyRGDrv.sys | 386431 | 天空 Co.，LTD. |
| SkyAMDrv.sys | 386430 | 天空 Co.，LTD. |
| SheedSelfProtection.sys | 386421 | SheedSoft Ltd |
| arta.sys | 386420 | SheedSoft ltd. |
| ApexSqlFilterDriver.sys | 386410 | ApexSQL LLC |
| stflt.sys | 386400 | Xacti |
| tbrdrv.sys | 386390 | 爬网程序组 |
| WinTeonMiniFilter.sys | 386320 | Dmitry Stefankov |
| wiper.sys | 386310 | Dmitry Stefankov |
| DevMonMiniFilter.sys | 386300 | Dmitry Stefankov |
| VMWVvpfsd.sys | 386200 | VMware，inc. |
| RTOLogon.sys （重命名） | 386200 | VMware，inc. |
| Code42Filter.sys | 386190 | Code42 |
| ConduantFSFltr.sys | 386180 | Conduant Corporation |
| KtFSFilter.sys | 386170 | Keysight 技术 |
| FileGuard.sys | 386140 | RES 软件 |
| NetGuard.sys | 386130 | RES 软件 |
| RegGuard.sys | 386120 | RES 软件 |
| ImgGuard.sys | 386110 | RES 软件 |
| AppGuard.sys | 386100 | RES 软件 |
| RuiDiskFs.sys | 386030 | RuiGuard Ltd |
| minitrc.sys | 386020 | 受保护的网络 |
| cpepmon.sys | 386010 | 检查点软件 |
| CGWMF.sys | 386000 | NetIQ |
| ISRegFlt.sys | 385990 | Flexera 软件 inc.保留所有权利。 |
| ISRegFlt64.sys | 385990 | Flexera 软件 inc.保留所有权利。 |
| shdlpSf.sys | 385970 | Comtrue 技术 |
| ctrPAMon.sys | 385960 | Comtrue 技术 |
| shdlpMedia.sys | 385950 | Comtrue 技术 |
| immflex.sys | 385910 | Immidio B.V. |
| StegoProtect.sys | 385900 | Stegosystems Inc |
| brfilter.sys | 385890 | Bromium Inc |
| BrCow_x_x_x_x.sys | 385889 | Bromium Inc |
| BemK.sys | 385888 | Bromium Inc |
| secRMM.sys | 385880 | Squadra 技术 |
| dgfilter.sys | 385870 | DataGravity inc.保留所有权利。 |
| WFP_MRT.sys | 385860 | FireEye Inc |
| klrsps.sys | 385815 | Kaspersky 实验室 |
| klsnsr.sys | 385810 | Kaspersky 实验室 |
| TaniumRecorderDrv.sys | 385800 | Tanium |
| mssecflt.sys | 385600 | Microsoft |
| Backupreader.sys | 385500 | Microsoft |
| MsixPackagingToolMonitor.sys | 385410 | Microsoft |
| AppVMon.sys | 385400 | Microsoft |
| DpmFilter.sys | 385300 | Microsoft |
| Procmon11.sys | 385200 | Microsoft |
| minispy.sys-顶部 | 385100 | Microsoft |
| fdrtrace.sys | 385001 | Microsoft |
| filetrace.sys | 385000 | Microsoft |
| uwfreg.sys | 384910 | Microsoft |
| uwfs.sys | 384900 | Microsoft |
| locksmith.sys | 384800 | Microsoft |
| winload.sys | 384700 | Microsoft |
| SFPMonitor.sys-顶部 | 383350 | SonicWall Inc |
| FilrDriver.sys | 383340 | Micro 焦点 |
| rwchangedrv.sys | 383330 | Rackware |
| airship filter.sys | 383320 | AIRWare 技术 Ltd |
| AeFilter.sys | 383310 | Faronics Corporation |
| QQProtect.sys | 383300 | 腾讯 （深圳） |
| QQProtectX64.sys | 383300 | 腾讯 （深圳） |
| KernelAgent32.sys | 383260 | ZoneFox |
| WRDWIZFILEPROT。SYS | 383251 | WardWiz |
| WRDWIZREGPROT。SYS | 383250 | WardWiz |
| groundling32.sys | 383200 | Dell Secureworks |
| groundling64.sys | 383200 | Dell Secureworks |
| avgtpx86.sys | 383190 | AVG 技术 CZ |
| avgtpx64.sys | 383190 | AVG 技术 CZ |
| DataNow_Driver.sys | 383182 | AppSense Ltd |
| UcaFltDriver.sys | 383180 | AppSense Ltd |
| YFSD2.sys | 383170 | Yokogawa Corpration |
| Kisknl.sys | 383160 | 软件 |
| MWatcher.sys | 383150 | Neowiz Corporation |
| tsifilemon.sys | 383140 | 对讲机 inc.保留所有权利。 |
| FIM.sys | 383130 | eIQnetworks inc.保留所有权利。 |
| cFSfdrv | 383120 | Chaewool |
| ajfsprot.sys | 383110 | Analytik Jena AG |
| isafermon | 383100 | (c)短信 |
| kfac.sys | 383000 | 北京 CA JinChen 软件 Co. |
| GUMHFilter.sys | 382910 | Glarysoft ltd. |
| PsAcFileAccessFilter.sys | 382902 | FUJITSU 软件 |
| FJGSDis2.sys | 382900 | FUJITSU LIMITED |
| secure_os.sys | 382890 | FUJITSU 社交科学 |
| ibr2fsk.sys | 382880 | FUJITSU 工程 |
| FJSeparettiFilterRedirect.sys | 382860 | FUJITSU LIMITED |
| Fsw31rj1.sys | 382855 | FUJITSU LIMITED |
| da_ctl.sys | 382850 | FUJITSU LIMITED |
| zqFilter.sys | 382800 | magrasoft Ltd |
| ntps_fa.sys | 382700 | NTP 软件 |
| sConnect.sys | 382600 | I/O 数据设备 |
| AdaptivaClientCache32.sys | 382500 | Adaptiva |
| AdaptivaclientCache64.sys | 382500 | Adaptiva |
| phantomd.sys | 382440 | Veramine Inc |
| GoFSMF.sys | 382430 | Gorizonty Rosta Ltd |
| SWCommFltr.sys | 382420 | SnoopWall LLC |
| atflt.sys | 382410 | Atlansys 软件 |
| amfd.sys | 382400 | Atlansys 软件 |
| iSafeKrnl.sys | 382390 | Elex 技术 Inc |
| iSafeKrnlMon.sys | 382380 | Elex 技术 Inc |
| Qutmdrv.sys | 382320 | 360 软件 （北京） |
| 360box.sys | 382310 | Qihoo 360 |
| 360fsflt.sys | 382300 | 北京 Qihoo 技术 Co. |
| scred.sys | 382210 | SoftCamp Co. |
| PDGenFam.sys | 382200 | Soluto LTD |
| MCFileMon64.sys (x 64 系统） | 382100 | 三井 Electric ltd. |
| MCFileMon32.sys (x 32 系统） | 382100 | 三井 Electric ltd. |
| RyGuard.sys | 382050 | 深圳 UNNOO 信息 Techco。 |
| FileShareMon.sys | 382040 | 深圳 UNNOO 信息 Techco。 |
| ryfilter.sys | 382030 | 深圳 UNNOO 信息 Techco。 |
| secufile.sys | 382020 | 深圳 Unnoo LTD |
| XiaobaiFs.sys | 382010 | 深圳 Unnoo LTD |
| XiaobaiFsR.sys | 382000 | 深圳 Unnoo LTD |
| TWBDCFilter.sys | 381910 | 开发 |
| VPDrvNt.sys | 381900 | AhnLab，inc. |
| eetd32.sys | 381800 | Entrust inc.保留所有权利 |
| eetd64.sys | 381800 | Entrust inc.保留所有权利 |
| dnaFSMonitor.sys | 381700 | Dtex 系统 |
| 在 2000 iwhlp2.sys | 381610 | InfoWatch |
| 在 XP 上 iwhlpxp.sys | 381610 | InfoWatch |
| 在 Vista 上 iwhlp.sys | 381610 | InfoWatch |
| iwdmfs.sys | 381600 | InfoWatch |
| IronGateFD.sys | 381500 | rubysoft |
| MagicBackupMonitor.sys | 381400 | Magic Softworks，inc. |
| Sonar.sys | 381337 | IKARUS 安全 |
| IPFilter.sys | 381310 | Jinfengshuntai |
| MSpy.sys | 381300 | Ladislav Zezula |
| inuse.sys | 381200 | 年 3 月一起共享软件 Ltd |
| qfmon.sys | 381190 | 质量 Corporation |
| flyfs.sys | 381160 | NEC 软 |
| serfs.sys | 381150 | NEC 软 |
| hdrfs.sys | 381140 | NEC 软 |
| UVMCIFSF.sys | 381130 | NEC Corporation |
| ICFClientFlt.sys | 381120 | NEC 系统技术，ltd. |
| IccFileIoAd.sys | 381110 | NEC 系统技术，ltd. |
| IccFilterAudit.sys | 381100 | NEC System 技术 |
| IccFilterSc.sys | 381090 | InfoCage |
| Sefo.sys-顶部 | 381010 | Solusseum Inc |
| mtsvcdf.sys | 381000 | CristaLink |
| SQLsafeFilterDriver.sys | 380901 | Idera 软件 |
| IderaFilterDriver.sys | 380900 | Idera |
| cbfsfilter2017.sys | 380850 | SN 系统 Ltd |
| xhunter1.sys | 380800 | Wellbia&#x2024;com |
| iGuard.sys | 380720 | i-Guard SAS |
| cbfltfs4.sys | 380715 | Nomadesk |
| cbfltfs4.sys | 380710 | 备份系统 Ltd |
| PkgFilter.sys | 380700 | 可缩放的软件 inc.保留所有权利。 |
| snimg.sys | 380600 | Softnext 技术 |
| SK.sys | 380520 | 热软件 |
| mpxmon.sys | 380510 | 正技术 |
| filenamevalidator.sys | 380502 | Infotecs |
| KC3.sys | 380500 | Infotecs |
| PLPOffDrv.sys | 380492 | SK Infosec Co |
| ISFPDrv.sys | 380491 | SK Infosec Co |
| ionmonwdrv.sys | 380490 | SK Infosec Co |
| Sefo.sys-中间 | 380480 | Solusseum Inc |
| sagntflt.sys | 380470 | ShinNihonSystec Co |
| VrExpDrv.sys | 380460 | Hauri Inc |
| srminifilterdrv.sys | 380450 | Citrix Systems |
| zzpensys.sys | 380440 | Zhuan Zhuan Jing Shen |
| tedrdrv.sys | 380430 | Palo Alto 网络 |
| fangcloud_autolock_driver.sys | 380420 | 杭州 Yifangyun |
| CbSampleDrv.sys | 380020 | Microsoft |
| CbSampleDrv.sys | 380010 | Microsoft |
| CbSampleDrv.sys | 380000 | Microsoft |
| simrep.sys | 371100 | Microsoft |
| change.sys | 370160 | Microsoft |
| delete_flt.sys | 370150 | Microsoft |
| SmbResilFilter.sys | 370140 | Microsoft |
| usbtest.sys | 370130 | Microsoft |
| NameChanger.sys | 370120 | Microsoft |
| failMount.sys | 370110 | Microsoft |
| failAttach.sys | 370100 | Microsoft |
| stest.sys | 370090 | Microsoft |
| cdo.sys | 370080 | Microsoft |
| ctx.sys | 370070 | Microsoft |
| fmm.sys | 370060 | Microsoft |
| cancelSafe.sys | 370050 | Microsoft |
| message.sys | 370040 | Microsoft |
| passThrough.sys | 370030 | Microsoft |
| nullFilter.sys | 370020 | Microsoft |
| ntest.sys | 370010 | Microsoft |
| minispy.sys-中间 | 370000 | Microsoft |
| isecureflt.sys | 368530 | iSecure ltd. |
| SFPMonitor.sys-中间 | 368520 | SonicWall Inc |
| wats_se.sys | 368510 | 福建 Shen 香港特别行政区 |
| secure_os_mf.sys | 368500 | HAURI |
| FileMonitor.sys | 368470 | Cygna 实验室 |
| asiofms.sys | 368460 | 鼓励技术 |
| cbfsfilter2017.sys | 368450 | 绝对软件 |
| FileHubAgent.sys | 368440 | SmartFile LLC |
| nrcomgrdki.sys | 368420 | NURILAB |
| nrcomgrdka.sys | 368420 | NURILAB |
| nrpmonki.sys | 368410 | NURILAB |
| nrpmonka.sys | 368410 | NURILAB |
| nravwka.sys | 368400 | NURILAB |
| bhkavki.sys | 368390 | NURILAB |
| bhkavka.sys | 368390 | NURILAB |
| docvmonk.sys | 368380 | NURILAB |
| docvmonk64.sys | 368380 | NURILAB |
| InvProtectDrv.sys | 368370 | Invincea |
| InvProtectDrv64.sys | 368370 | Invincea |
| browserMon.sys | 368360 | Adtrustmedia |
| SfdFilter.sys | 368350 | Sandoll 通信 |
| phdcbtdrv.sys | 368340 | 博士虚拟技术 inc.保留所有权利。 |
| sysdiag.sys | 368330 | HeroBravo 技术 |
| CmdCwagt.sys | 368322 | Comodo 安全解决方案 inc.保留所有权利。 |
| cfrmd.sys | 368320 | Comodo 安全解决方案 inc.保留所有权利。 |
| repdrv.sys | 368310 | 视觉解决方案 |
| repmon.sys | 368300 | 视觉解决方案 |
| cvofflineFlt32.sys | 368200 | 量程 Corporation。 |
| cvofflineFlt64.sys | 368200 | 量程 Corporation。 |
| DsDriver.sys | 368100 | Warp 磁盘软件 |
| nlcbhelpx86.sys | 368000 | NetLib |
| nlcbhelpx64.sys | 368000 | NetLib |
| nlcbhelpi64.sys | 368000 | NetLib |
| wbfilter.sys | 367950 | 白盒安全 |
| LRAgentMF.sys | 367900 | LogRhythm inc.保留所有权利。 |
| Drwebfwflt.sys | 367810 | 医生 Web |
| EventMon.sys | 367800 | 医生 Web |
| dsfltfs.sys | 367760 | Digitalsense Co |
| soidriver.sys | 367750 | Sophos Plc |
| drvhookcsmf.sys | 367700 | GrammaTech，inc. |
| drvhookcsmf_amd64.sys | 367700 | GrammaTech，inc. |
| avipbb.sys | 367600 | Avira GmbH |
| FileSightMF.sys | 367500 | PA 文件建立直通连接， |
| csaam.sys | 367400 | Cisco 系统 |
| FSMon.sys | 367300 | 1mill |
| filefilter.sys | 367100 | 北京 Zhong 挂起 Jiaxin 计算机网络科技有限公司 |
| iiscache.sys | 367000 | Microsoft |
| nowonmf.sys | 366993 | 为 diskeeper Corporation |
| dktlfsmf.sys | 366992 | 为 diskeeper Corporation |
| DKDrv.sys | 366991 | 为 diskeeper Corporation |
| DKRtWrt.sys-XPSP3 临时修复 | 366990 | 为 diskeeper Corporation |
| HBFSFltr.sys | 366980 | 为 diskeeper Corporation |
| xoiv8x64.sys | 366940 | Arcserve |
| xomfcbt8x64.sys | 366930 | CA |
| KmxAgent.sys | 366920 | CA |
| KmxFile.sys | 366910 | CA |
| KmxSbx.sys | 366900 | CA |
| PointGuardVistaR32.sys | 366810 | Futuresoft |
| PointGuardVistaR64.sys | 366810 | Futuresoft |
| PointGuardVistaF.sys | 366800 | Futuresoft |
| PointGuardVista64F.sys | 366800 | Futuresoft |
| vintmfs.sys | 366789 | CondusivTechnologies |
| hiofs.sys | 366782 | Condusiv 技术 |
| intmfs.sys | 366781 | CondusivTechnologies |
| excfs.sys | 366780 | CondusivTechnologies |
| zampit_ml.sys | 366700 | Zampit |
| tesxnginx.sys | 366666 | 腾讯技术 |
| rflog.sys | 366600 | 应用程序流，inc. |
| csmon.sys | 366582 | CyberSight Inc |
| mumdi.sys | 366540 | ZenmuTech inc.保留所有权利。 |
| LivedriveFilter.sys | 366500 | Livedrive Internet Ltd |
| regmonex.sys | 366410 | Tranxition Corp |
| TXRegMon.sys | 366400 | Tranxition Corp |
| SDVFilter.sys | 366300 | Soliton 系统 K.K. |
| eLock2FSCTLDriver.sys | 366210 | Egis 技术 inc.保留所有权利。 |
| msiodrv4.sys | 366200 | Centennial 软件 Ltd |
| mmPsy32.sys | 366110 | Resplendence 软件项目 |
| mmPsy64.sys | 366110 | Resplendence 软件项目 |
| rrMon32.sys | 366100 | Resplendence 软件项目 |
| rrMon64.sys | 366100 | Resplendence 软件项目 |
| cvsflt.sys | 366000 | 年 3 月一起共享软件 Ltd |
| ktsyncfsflt.sys | 365920 | KnowledgeTree inc.保留所有权利。 |
| nvmon.sys | 365900 | NetVision，inc. |
| SnDacs.sys | 365810 | Informzaschita |
| SnExequota.sys | 365800 | Informzaschita |
| llfilter.sys | 365700 | SecureAxis 软件 |
| hafsnk.sys | 365660 | HA Unix Pt |
| DgeDriver.sys | 365655 | Dell Software Inc. |
| BWFSDrv.sys | 365650 | Quest Software Inc. |
| CAADFlt.sys | 365601 | Quest Software Inc. |
| QFAPFlt.sys | 365600 | Quest Software |
| XendowFLT.sys | 365570 | Credant 技术 |
| fmdrive.sys | 365500 | Cigital，inc. |
| EGMinFlt.sys | 365400 | WhiteCell 软件 inc.保留所有权利。 |
| it2reg.sys | 365315 | Soliton 系统 |
| it2drv.sys | 365310 | Soliton 系统 |
| solitkm.sys | 365300 | Soliton 系统 |
| pgpwdefs.sys | 365270 | Symantec |
| GEProtection.sys | 365260 | Symantec |
| diflt.sys | 365260 | Symantec corp. |
| sysMon.sys | 365250 | Symantec |
| ssrfsf.sys | 365210 | Symantec |
| emxdrv2.sys | 365200 | Symantec |
| reghook.sys | 365150 | Symantec |
| symevnt.sys | 365110 | Symantec |
| spbbcdrv.sys | 365100 | Symantec |
| bhdrvx86.sys | 365100 | Symantec |
| bhdrvx64.sys | 365100 | Symantec |
| SISIPSFileFilter | 365010 | Symantec |
| symevent.sys | 365000 | Symantec |
| wrpfv.sys | 364900 | Microsoft |
| UpGuardRealTime.sys | 364810 | UpGuard |
| usbl_ifsfltr.sys | 364800 | SecureAxis |
| ntfsf.sys | 364700 | Sun 和木增加 |
| BssAudit.sys | 364600 | ByStorm |
| GPMiniFIlter.sys | 364500 | Kalpataru |
| AlfaFF.sys | 364400 | Alfa |
| FSAFilter.sys | 364300 | 试一下 ScriptLogic |
| GcfFilter.sys | 364200 | GemacmbH |
| FFCFILT。SYS | 364100 | FFC Limited |
| msnfsflt.sys | 364000 | Microsoft |
| mblmon.sys | 363900 | Packeteer |
| amsfilter.sys | 363800 | Axur 信息数秒。 |
| rswctrl.sys | 363713 | Douzone Bizon Co |
| mcstrg.sys | 363712 | Douzone Bizon Co |
| fmkkc.sys | 363711 | Douzone Bizon Co |
| nmlhssrv01.sys | 363710 | Douzone Bizon Co |
| equ8_helper.sys | 363705 | Int3 软件 AB |
| strapvista.sys （已停用） | 363700 | AvSoft 技术 |
| 安全 Agent.sys | 363636 | 安全 Cyberdefense |
| EstPrmon.sys | 363610 | ESTsoft corp。 |
| Estprp.sys-64 位 | 363610 | ESTsoft corp。 |
| EstRegmon.sys | 363600 | ESTsoft corp。 |
| EstRegp.sys-64 位 | 363600 | ESTsoft corp。 |
| agfsmon.sys | 363530 | TechnoKom ltd. |
| NlxFF.sys | 363520 | OnGuard 系统 LLC |
| Sahara.sys | 363511 | Safend |
| Santa.sys | 363510 | Safend |
| vfdrv.sys | 363500 | Viewfinity |
| topdogfsfilt.sys | 363450 | ManTech |
| xhunter64.sys | 363400 | Wellbia&#x2024;com |
| uncheater.sys | 363390 | Wellbia&#x2024;com |
| AuditFlt.sys | 363313 | Ionx 解决方案 LLP |
| SPIMiniFilter.sys | 363300 | 软件需要 inc.保留所有权利。 |
| mracdrv.sys | 363230 | Mail&#x2024;Ru |
| BEDaisy.sys | 363220 | BattlEye 创新 |
| NetAccCtrl.sys | 363200 | 链接 co。 |
| NetAccCtrl64.sys | 363200 | 链接 co。 |
| hpreg.sys | 363130 | HP |
| qfimdvr.sys | 363120 | Qualys inc.保留所有权利。 |
| QDocumentREF.sys | 363110 | BicDroid inc.保留所有权利。 |
| dsfemon.sys | 363100 | 拓扑 Ltd |
| AmznMon.sys | 363030 | Amazon Web Services Inc |
| iothorfs.sys | 363020 | ioScience |
| ctamflt.sys | 363010 | ComTrade |
| psisolator.sys | 363000 | SharpCrafters |
| QmInspec.sys | 362990 | 北京 QiAnXin 技术。 |
| GagSecurity.sys | 362970 | 北京 Shu Yan 科学 |
| CybKernelTracker.sys | 362960 | CyberArk 软件 |
| filemon.sys | 362950 | Temasoft 公司 |
| SCAegis.sys | 362940 | Sogou ltd. |
| fpifp_minifilter.sys | 362930 | ForcePoint LLC。 |
| klifks.sys | 362902 | Kaspersky 实验室 |
| klifaa.sys | 362901 | Kaspersky 实验室 |
| Klifsm.sys | 362900 | Kaspersky 实验室 |
| nxrmflt.sys | 362860 | NextLabs |
| vast.sys | 362850 | PolyLogyx LLC |
| AALProtect.sys | 362840 | AlphaAntiLeak |
| egnfsflt.sys | 362830 | Egnyte Inc |
| RsFlt.sys | 362820 | Redstor Limited |
| CentrifyFSF.sys | 362810 | Centrify Corp |
| Sefo.sys-底部 | 362800 | Solusseum Inc |
| SFPMonitor.sys-底部 | 362700 | SonicWall Inc |
| minispy.sys-底部 | 361000 | Microsoft |

## <a name="span-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespan340000---349999-fsfilter-undelete"></a><span id="340000_-_349999__FSFilter_Undelete"></span><span id="340000_-_349999__fsfilter_undelete"></span><span id="340000_-_349999__FSFILTER_UNDELETE"></span>340000-349999:FSFilter 撤消删除

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| BSSFlt.sys | 346000 | 蓝色 Shoe 软件 LLC |
| ThinIO.sys | 345900 | ThinScale 技术 |
| hmpalert.sys | 345800 | SurfRight |
| nsffkmd64.sys | 345700 | NetSTAR inc.保留所有权利。 |
| nsffkmd32.sys | 345700 | NetSTAR inc.保留所有权利。 |
| xbprocfilter.sys | 345600 | Zrxb |
| ifileguard.sys | 345500 | I/O 数据设备，INC. |
| undelex32.sys | 345400 | Resplendence 软件项目 |
| undelex64.sys | 345400 | Resplendence 软件项目 |
| starmon.sys | 345300 | Kantowitz 工程，inc. |
| mxRCycle.sys | 345200 | Avanquest |
| UdFilter.sys | 345100 | 为 diskeeper Corporation |
| it2prtc.sys | 345040 | Soliton 系统 K.K. |
| SolRegFilter.sys | 345030 | Soliton 系统 K.K. |
| SolSecBr.sys | 345020 | Soliton 系统 K.K. |
| SolFCLLi.sys | 345010 | Soliton 系统 K.K. |
| SolFCL.sys | 345000 | Soliton 智能秒 |
| DCVPr.sys | 340700 | SecurStar GmbH |

## <a name="span-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspan320000---329998-fsfilter-anti-virus"></a><span id="320000_-_329998__FSFilter_Anti-Virus"></span><span id="320000_-_329998__fsfilter_anti-virus"></span><span id="320000_-_329998__FSFILTER_ANTI-VIRUS"></span>320000-329998:FSFilter 防病毒软件

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| zwPxeSvr.sys | 329330 | SecureLink inc.保留所有权利。 |
| zwASatom.sys | 329320 | SecureLink inc.保留所有权利。 |
| wscm.sys | 329310 | Fujitsu 社会科学 |
| IMFFilter.sys | 329300 | IObit 信息技术 |
| CSFlt.sys | 329290 | ConeSecurity Inc |
| ospfile_mini.sys | 329230 | OKUMA Corp |
| SoftFilterxxx.sys | 329222 | WidgetNuri Corp |
| RansomDefensexxx.sys | 329220 | WidgetNuri Corp |
| RanPodFS.sys | 329210 | Pooyan 系统 |
| ksfsflt.sys | 329200 | 北京软件 |
| DeepInsFS.sys | 329190 | 深度想到 |
| AppCheckD.sys | 329180 | CheckMAL Inc |
| spellmon.sys | 329170 | SpellSecurity |
| WhiteShield.sys | 329160 | Meidensha Corp |
| reaqtor.sys | 329150 | ReaQta ltd. |
| SE46Filter.sys | 329140 | 技术 Nexus AB |
| FileScan.sys | 329130 | NPcore Ltd |
| ECATDriver.sys | 329120 | EMC |
| pfkrnl.sys | 329110 | FXSEC LTD |
| epicFilter.sys | 329100 | 隐藏的单反 |
| b9kernel.sys | 329050 | Bit9 Inc |
| eeCtrl.sys | 329010 | Symantec |
| eraser.sys （已停用） | 329010 | Symantec |
| SRTSP.sys | 329000 | Symantec |
| SRTSPIT.sys-ia64 系统 | 329000 | Symantec |
| SRTSP64。SYS-x64 系统 | 329000 | Symantec |
| a2ertpx86.sys | 328920 | 将 Emsi 软件 GmbH |
| a2ertpx64.sys | 328920 | 将 Emsi 软件 GmbH |
| a2gffx86.sys-x86 | 328910 | 将 Emsi 软件 GmbH |
| a2gffx64.sys-x64 | 328910 | 将 Emsi 软件 GmbH |
| a2gffi64.sys 的 IA64 | 328910 | 将 Emsi 软件 GmbH |
| a2acc.sys | 328900 | 将 Emsi 软件 GmbH |
| 在 x64 上的 a2acc64.sys 系统 | 328900 | 将 Emsi 软件 GmbH |
| FlightRecorder.sys | 328850 | Malwarebytes corp. |
| si32_file.sys | 328810 | Scargo Inc |
| si64_file.sys | 328810 | Scargo Inc |
| mbam.sys | 328800 | Malwarebytes corp. |
| EnigmaFileMonDriver.sys | 328770 | EnigmaSoft |
| KUBWKSP.sys | 328750 | Netlor SAS |
| hcp_kernel_acq.sys | 328740 | refractionPOINT |
| SegiraFlt.sys | 328730 | Segira LLC |
| wdocsafe.sys | 328722 | Cheetah 移动 inc.保留所有权利。 |
| lbprotect.sys | 328720 | Cheetah 移动 inc.保留所有权利。 |
| eamonm.sys | 328700 | 重置，spol。 s r.o. |
| klam.sys | 328650 | Kaspersky 实验室 |
| MaxProc64.sys | 328620 | 最大安全软件 |
| MaxProtector.sys | 328610 | 最大安全软件 |
| maxcryptmon.sys | 328601 | 最大安全软件 |
| SDActMon.sys | 328600 | 最大安全软件 |
| fileflt.sys | 328540 | Trend Micro inc.保留所有权利。 |
| TmEsFlt.sys | 328530 | Trend Micro inc.保留所有权利。 |
| TmEyes.sys | 328520 | Trend Micro inc.保留所有权利。 |
| tmevtmgr.sys | 328510 | Trend Micro inc.保留所有权利。 |
| tmpreflt.sys | 328500 | 趋势 |
| vcMFilter.sys | 328400 | SGRI Co.，LTD. |
| SAFsFilter.sys | 328300 | Lightspeed Systems inc.保留所有权利。 |
| vsepflt.sys | 328200 | VMware，inc. |
| VFileFilter.sys(renamed) | 328200 | VMware，inc. |
| sfavflt.sys | 328130 | Sangfor 技术 |
| sfavflt.sys | 328120 | Sangfor 技术 |
| drivesentryfilterdriver2lite.sys | 328100 | DriveSentry Inc |
| WdFilter.sys | 328010 | Microsoft |
| mpFilter.sys | 328000 | Microsoft |
| vrSDetri.sys | 327801 | ETRI |
| vrSDetrix.sys | 327800 | ETRI |
| AhkSvPro.sys | 327720 | Ahkun Co. |
| AhkUsbFW.sys | 327710 | Ahkun Co. |
| AhkAMFlt.sys | 327700 | Ahkun Co. |
| PSINPROC。SYS | 327620 | Panda 安全 |
| PSINFILE。SYS | 327610 | Panda 安全 |
| amfsm.sys-Windows XP/2003 x64 | 327600 | Panda 安全 |
| amm8660.sys-Windows Vista x86 | 327600 | Panda 安全 |
| amm6460.sys-Windows Vista x64 | 327600 | Panda 安全 |
| ADSpiderDoc.sys | 327550 | Digitalonnet |
| BkavAutoFlt.sys | 327542 | Bkav Corporation |
| BkavSdFlt.sys | 327540 | Bkav Corporation |
| easyanticheat.sys | 327530 | EasyAntiCheat 解决方案 |
| 5nine.cbt.sys | 327520 | 5nine 软件 inc.保留所有权利。 |
| caavFltr.sys | 327510 | 计算机 Assoc |
| ino_fltr.sys | 327500 | 计算机 Assoc |
| SECOne_USB.sys | 327426 | GRGBanking 设备 |
| SECOne_Proc10.sys | 327424 | GRGBanking 设备 |
| SECOne_REG10.sys | 327422 | GRGBanking 设备 |
| SECOne_FileMon10.sys | 327420 | GRGBanking 设备 |
| WCSDriver.sys | 327410 | 白色云安全 |
| 360qpesv.sys | 327404 | 360 软件 （北京） |
| dsark.sys | 327402 | Qihoo 360 |
| 360avflt.sys | 327400 | Qihoo 360 |
| scifsflt.sys | 327333 | SECUI Corporation |
| ANVfsm.sys | 327310 | Arcdo |
| CDrRSFlt.sys | 327300 | Arcdo |
| mfdriver.sys | 327250 | Imperva inc.保留所有权利。 |
| EPSMn.sys | 327200 | 总务 |
| VTSysFlt.sys | 327150 | 北京 Venus |
| TesMon.sys | 327130 | 腾讯 |
| QQSysMonX64.sys | 327125 | 腾讯 |
| QQSysMon.sys | 327120 | 腾讯 |
| TSysCare.sys | 327110 | 深圳腾讯计算机系统公司限制 |
| TFsFlt.sys | 327100 | 深圳腾讯计算机系统公司限制 |
| avmf.sys | 327000 | Authentium |
| BDFileDefend.sys | 326916 | 百度 （北京） |
| BDsdKit.sys | 326914 | 百度联机网络技术 （北京） Co. |
| bd0003.sys | 326912 | 百度联机网络技术 （北京） Co. |
| Bfilter.sys | 326910 | 有限的百度 （中国香港特别行政区） |
| NeoKerbyFilter | 326900 | NeoAutus |
| egnfsflt.sys | 326830 | Egnyte Inc |
| RsFlt.sys | 326820 | Redstor Limited |
| trpmnflt.sys | 326810 | TRAPMINE A.S. |
| PLGFltr.sys | 326800 | Paretologic |
| WrdWizSecure64.sys | 326730 | WardWiz |
| wrdwizscanner.sys | 326720 | WardWiz |
| AshAvScan.sys | 326700 | Ashampoo GmbH & Co.KG |
| Zyfm.sys | 326666 | ZhengYong InfoTech ltd. |
| csaav.sys | 326600 | Cisco 系统 |
| oavfm.sys | 326550 | HSM IT 服务 Gmbh |
| SegMD.sys | 326520 | Segurmatica |
| SegMP.sys | 326510 | Segurmatica |
| SegF.sys | 326500 | Segurmatica |
| eeyehv.sys | 326400 | eEye 数字安全 |
| eeyehv64.sys | 326400 | eEye 数字安全 |
| CpAvFilter.sys | 326311 | CodeProof 技术 Inc |
| CpAvKernel.sys | 326310 | CodeProof 技术 Inc |
| NovaShield.sys | 326300 | Securitas Technologies，inc. |
| SheedAntivirusFilterDriver.sys | 326290 | SheedSoft Ltd |
| bSyirmf.sys | 326260 | BLACKFORT 安全 |
| bSysp.sys | 326250 | BLACKFORT 安全 |
| bSymfdm.sys | 326240 | BLACKFORT 安全 |
| bSywl.sys | 326235 | BLACKFORT 安全 |
| bSyrtm.sys | 326230 | BLACKFORT 安全 |
| bSyaed.sys | 326220 | BLACKFORT 安全 |
| bSyar.sys | 326210 | BLACKFORT 安全 |
| BdFileSpy.sys | 326200 | BullGuard |
| npxgd.sys | 326160 | INCA Internet Co. |
| npxgd64.sys | 326160 | INCA Internet Co. |
| tkpl2k.sys | 326150 | INCA Internet Co. |
| tkpl2k64.sys | 326150 | INCA Internet Co. |
| GKFF.sys | 326140 | INCA Internet Co. |
| GKFF64.sys | 326140 | INCA Internet Co. |
| tkdac2k.sys | 326130 | INCA Internet Co. |
| tkdacxp.sys | 326130 | INCA Internet Co. |
| tkdacxp64.sys | 326130 | INCA Internet Co. |
| tksp2k.sys | 326120 | INCA Internet Co. |
| tkspxp.sys | 326120 | INCA Internet Co. |
| tkspxp64.sys | 326120 | INCA Internet Co. |
| tkfsft.sys | 326110 | INCA Internet Co.，Ltd |
| tkfsft64.sys-64 位 | 326110 | INCA Internet Co.，Ltd |
| tkfsavxp.sys-32 位 | 326100 | INCA Internet Co.，Ltd |
| tkfsavxp64.sys-64 位 | 326100 | INCA Internet Co.，Ltd |
| SMDrvNt.sys | 326040 | AhnLab，inc. |
| ATamptNt.sys | 326030 | AhnLab，inc. |
| V3Flt2k.sys | 326020 | AhnLab，inc. |
| V3MifiNt.sys | 326010 | Ahnlab |
| V3Ift2k.sys | 326000 | Ahnlab |
| V3IftmNt.sys （旧名称） | 326000 | Ahnlab |
| ArfMonNt.sys | 325990 | Ahnlab |
| AhnRghLh.sys | 325980 | Ahnlab |
| AszFltNt.sys | 325970 | Ahnlab |
| OMFltLh.sys | 325960 | Ahnlab |
| V3Flu2k.sys | 325950 | Ahnlab |
| TfFregNt.sys | 325940 | AhnLab inc.保留所有权利。 |
| AdcVcsNT.sys | 325930 | Ahnlab |
| vcdriv.sys | 325820 | Greatsoft Corp.Ltd |
| vcreg.sys | 325810 | Greatsoft Corp.Ltd |
| vchle.sys | 325800 | Greatsoft Corp.Ltd |
| NxFsMon.sys | 325700 | Novatix Corporation |
| AntiLeakFilter.sys | 325600 | 单个开发人员 (Soft3304) |
| NanoAVMF.sys | 325510 | Panda 软件 |
| shldflt.sys | 325500 | Panda 软件 |
| nprosec.sys | 325410 | Norman ASA |
| nregsec.sys | 325400 | Norman ASA |
| issregistry.sys | 325300 | IBM |
| THFilter.sys | 325200 | Sybonic 系统 Inc |
| pervac.sys | 325100 | PerSystems SA |
| avgmfx86.sys | 325000 | AVG Grisoft |
| avgmfx64.sys | 325000 | AVG Grisoft |
| avgmfi64.sys | 325000 | AVG Grisoft |
| avgmfrs.sys （已停用） | 325000 | AVG Grisoft |
| FortiAptFilter.sys | 324930 | Fortinet inc.保留所有权利。 |
| fortimon2.sys | 324920 | Fortinet inc.保留所有权利。 |
| fortirmon.sys | 324910 | Fortinet inc.保留所有权利。 |
| fortishield.sys | 324900 | Fortinet inc.保留所有权利。 |
| mscan rt.sys | 324800 | SecureBrain Corporation |
| sysdiag.sys | 324600 | Huorong 安全 |
| agentrtm64.sys | 324510 | WINS CO。 LTD |
| rswmon.sys | 324500 | WINS CO。 LTD |
| mwfsmfltr.sys | 324420 | MicroWorld 软件服务 Pvt。 Ltd. |
| gtkdrv.sys | 324410 | GridinSoft LLC |
| GbpKm.sys | 324400 | 天然气 Tecnologia |
| crnsysm.sys | 324310 | Coranti inc.保留所有权利。 |
| crncache32.sys | 324300 | Coranti inc.保留所有权利。 |
| crncache64.sys | 324300 | Coranti inc.保留所有权利。 |
| egambit.sys | 324242 | TEHTRI 安全 |
| drwebfwft.sys | 324210 | 医生 Web |
| DwShield.sys | 324200 | 医生 Web |
| DwShield64.sys | 324200 | 医生 Web |
| IProtect.sys | 324150 | EveryZone inc.保留所有权利。 |
| TvFiltr.sys | 324140 | EveryZone inc.保留所有权利。 |
| TvDriver.sys | 324130 | EveryZone inc.保留所有权利。 |
| TvSPFltr.sys | 324120 | EveryZone inc.保留所有权利。 |
| TvPtFile.sys | 324110 | EveryZone inc.保留所有权利。 |
| TvMFltr.sys | 324100 | Everyzone |
| SophosED.sys | 324050 | Sophos |
| SAVOnAccess.sys | 324010 | Sophos |
| savonaccess.sys | 324000 | Sophos |
| sld.sys | 323990 | Sophos |
| OADevice.sys | 323900 | 高 Emu |
| pwipf6.sys | 323800 | PWI，inc. |
| EstRkmon.sys | 323700 | ESTsoft corp。 |
| EstRkr.sys-64 位 | 323700 | ESTsoft corp。 |
| dwprot.sys | 323610 | 医生 Web |
| Spiderg3.sys | 323600 | 医生 Web ltd. |
| STKrnl64.sys | 323500 | Verdasys Inc |
| UFDFilter.sys | 323400 | Yoggie |
| SCFltr.sys | 323300 | SecurityCoverage，inc. |
| fildds.sys | 323200 | Filseclab |
| fsfilter.sys | 323100 | MastedCode Ltd |
| fpav_rtp.sys | 323000 | f 保护 |
| cwdriver.sys | 322900 | Leith 条形码 |
| AYFilter.sys | 322810 | ESTsoft |
| Rtw.sys | 322800 | ESTsoft |
| RSRtw.sys | 322790 | ESTsecurity Corp |
| RSPCRtw.sys | 322780 | ESTsecurity Corp |
| HookSys.sys | 322700 | 北京上升信息技术公司限制 |
| snscore.sys | 322600 | S.N.Safe 和软件 |
| ssvhook.sys | 322500 | SecuLution GmbH |
| strapvista.sys | 322400 | AvSoft 技术 |
| strapvista64.sys | 322400 | AvSoft 技术 |
| sascan.sys | 322300 | SecureAge 技术 |
| savant.sys | 322200 | Savant 保护，inc. |
| VrARnFlt.sys | 322161 | HAURI |
| VrBBDFlt.sys | 322160 | HAURI |
| vrSDfmx.sys | 322153 | HAURI |
| vrSDfmx.sys | 322152 | HAURI |
| vrSDam.sys | 322151 | HAURI |
| vrSDam.sys | 322150 | HAURI |
| VRAPTFLT.sys | 322140 | HAURI inc.保留所有权利。 |
| VrAptDef.sys | 322130 | HAURI |
| VrSdCore.sys | 322120 | HAURI |
| VrFsFtM.sys | 322110 | HAURI |
| VrFsFtMX.sys(AMD64) | 322110 | HAURI |
| vradfil2.sys | 322100 | HAURI |
| fsgk.sys | 322000 | f 安全 |
| bouncer.sys | 321950 | CoreTrace Corporation |
| PCTCore64.sys | 321910 | PC 工具 Pty. Ltd. |
| PCTCore.sys （旧名称） | 321910 | PC 工具 Pty. Ltd. |
| ikfilesec.sys | 321900 | PC 工具 Pty. Ltd. |
| ZxFsFilt.sys | 321800 | 澳大利亚项目 |
| antispyfilter.sys | 321700 | C NetMedia Inc |
| PZDrvXP.sys | 321600 | VisionPower Co.，Ltd. |
| ggc.sys | 321510 | 快速修复 TechnologiesPvt。 Ltd. |
| catflt.sys | 321500 | 快速修复 TechnologiesPvt。 Ltd. |
| bdsflt.sys | 321490 | 快速修复技术 Pvt。 Ltd. |
| arwflt.sys | 321480 | 快速修复技术 Pvt。 Ltd. |
| csagent.sys | 321410 | CrowdStrike ltd. |
| kmkuflt.sys | 321400 | Komoku inc.保留所有权利。 |
| ntguard.sys | 321337 | IKARUS 安全 |
| epdrv.sys | 321320 | McAfee inc.保留所有权利。 |
| mfencoas.sys | 321310 | McAfee inc.保留所有权利。 |
| mfehidk.sys | 321300 | McAfee inc.保留所有权利。 |
| swin.sys | 321250 | McAfee inc.保留所有权利。 |
| CyvrFsfd.sys | 321234 | Palo Alto 网络 |
| cmdccav.sys | 321210 | Comodo Group 有限公司 |
| cmdguard.sys | 321200 | Comodo Group 有限公司 |
| K7Sentry.sys | 321100 | K7 计算私有 ltd. |
| nsminflt.sys | 321050 | NHN |
| nsminflt64.sys | 321050 | NHN |
| nvcmflt.sys | 321000 | Norman |
| dgsafe.sys | 320950 | 软件 |
| issfltr.sys | 320900 | ISS |
| hbflt.sys | 320840 | BitDefender SRL |
| bdsvm.sys | 320830 | Bitdefender |
| gzflt.sys | 320820 | BitDefender SRL |
| bddevflt.sys | 320812 | BitDefender SRL |
| ignis.sys | 320811 | BitDefender SRL |
| AVCKF。SYS | 320810 | BitDefender SRL |
| bdfsfltr.sys | 320800 | Softwin |
| bdfm.sys | 320790 | Softwin |
| gemma.sys | 320782 | BitDefender SRL |
| Atc.sys | 320781 | BitDefender SRL |
| AVC3。SYS | 320780 | BitDefender SRL |
| TRUFOS。SYS | 320770 | BitDefender SRL |
| aswmonflt.sys | 320700 | Alwil |
| HookCentre.sys | 320602 | G 数据 |
| PktIcpt.sys | 320601 | G 数据 |
| MiniIcpt.sys | 320600 | G 数据 |
| avgntflt.sys | 320500 | Avira GmbH |
| klam.sys | 320450 | Kaspersky 实验室 |
| klbg.sys | 320440 | Kaspersky |
| kldback.sys | 320430 | Kaspersky |
| kldlinf.sys | 320420 | Kaspersky |
| kldtool.sys | 320410 | Kaspersky |
| klif.sys | 320401 | Kaspersky 实验室 |
| klif.sys | 320400 | Kaspersky |
| klam.sys | 320350 | Kaspersky 实验室 |
| hsmltwhl.sys | 320340 | 人： Hitachi Solutions |
| hssfwhl.sys | 320330 | 人： Hitachi Solutions |
| DeepInsFS.sys | 320320 | 深度想到 ltd. |
| avfsmn.sys | 320310 | Anvisoft |
| lbd.sys | 320300 | Lavasoft AB |
| pavdrv.sys | 320210 | Panzor 网络安全 |
| rvsmon.sys | 320200 | CJSC Returnil 软件 |
| WRKrn.sys | 320110 | Webroot inc.保留所有权利。 |
| ssfmonm.sys | 320100 | Webroot 软件，inc. |
| vk_fsf.sys | 320050 | AxBx |
| VirtualAgent.sys | 320005 | Symantec |

## <a name="span-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspan300000---309998-fsfilter-replication"></a><span id="300000_-_309998__FSFilter_Replication"></span><span id="300000_-_309998__fsfilter_replication"></span><span id="300000_-_309998__FSFILTER_REPLICATION"></span>300000-309998:FSFilter 复制

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| IntelCAS.sys | 309100 | Intel Corporation |
| mvfs.sys | 309000 | IBM Corporation |
| frxccd.sys | 306000 | FSLogix inc.保留所有权利。 |
| fsrecord.sys | 305000 | Microsoft |
| InstMon.sys | 304201 | Numecent inc.保留所有权利。 |
| StreamingFSD.sys | 304200 | Numecent inc.保留所有权利。 |
| ubcminifilterdriver.sys | 304100 | Ullmore ltd. |
| replistor.sys | 304000 | Legato |
| stfsd.sys | 303900 | 工作技术 |
| xomf.sys | 303800 | CA (XOSOFT) |
| nfid.sys | 303700 | 从不组 Ltd |
| sybfilter.sys | 303600 | Sybase，inc.保留所有权利。 |
| rfsfilter.sys | 303500 | Evidian |
| cvmfsj.sys | 303400 | CommVault Systems，inc.保留所有权利。 |
| iOraFilter.sys | 303300 | Infonic plc |
| bkbmfd32.sys (x86) | 303200 | BakBone 软件，Inc |
| bkbmfd64.sys (x64) | 303200 | BakBone 软件，Inc |
| mblvn.sys | 303100 | Packeteer |
| AV12NFNT.sys | 303000 | AhnLab |
| mDP_win_mini.sys | 302900 | 宏的影响 |
| ctxubs.sys | 302800 | Citrix Systems inc.保留所有权利。 |
| rrepfsf.sys | 302700 | Rose 数据系统 Inc |
| cbfsfilter2017.sys | 301900 | 非常灵活的软件 |
| AxFilter.sys | 301800 | Axcient inc.保留所有权利。 |
| vxfsrep.sys | 301700 | Symantec |
| dellcapfd.sys | 301600 | Dell Inc. |
| Sptres.sys | 301500 | Safend |
| OfficeBackup.sys | 301400 | Ushus 技术 |
| pcvnfilt.sys | 301300 | Blue Coat |
| repdac.sys | 301200 | NSI |
| repkap.sys | 301100 | NSI |
| repdrv.sys | 301000 | NSI |

## <a name="span-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspan280000---289998-fsfilter-continuous-backup"></a><span id="280000_-_289998__FSFilter_Continuous_Backup"></span><span id="280000_-_289998__fsfilter_continuous_backup"></span><span id="280000_-_289998__FSFILTER_CONTINUOUS_BACKUP"></span>280000-289998:FSFilter 持续备份

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| Klcdp.sys | 288900 | Kaspersky 实验室 |
| splitinfmon.sys | 288800 | 拆分无穷大 |
| versamatic.sys | 288700 | Acertant 技术 |
| Yfilemon.sys | 288690 | Yarisoft |
| ibac.sys | 288600 | Idealstor，LLC。 |
| fkdriver.sys | 288500 | Filekeeper |
| AAFileFilter.sys | 288300 | Dell Inc. |
| hyperoo.sys | 288400 | Hyperoo Ltd |
| HyperBacCA.sys | 285000 | Red Gate 软件 Ltd |
| ZMSFsFltr.sys | 284400 | 全盛 InfoTech |
| AlfaSC.sys | 284300 | Alfa Corporation |
| hie_ifs.sys | 284200 | Hie 电子设备，inc. |
| AAFs.sys | 284100 | AppAssure 软件 |
| defilter.sys （旧版） | 284000 | Microsoft |
| aFsvDrv.sys | 283100 | ITSTATION Inc |
| tilana.sys | 283000 | Tilana Sys |
| VmDPFilter.sys | 282900 | 宏的影响 |
| LbFilter.sys | 281700 | Linkverse 公司 |
| fbsfd.sys | 281600 | Ferro 软件 |
| dupleemf.sys | 281500 | Duplee SPI，s.l。 |
| file_tracker.sys | 281420 | Acronis inc.保留所有权利。 |
| exbackup.sys | 281410 | Acronis inc.保留所有权利。 |
| afcdp.sys | 281400 | Acronis inc.保留所有权利。 |
| dcefltr.sys | 281300 | Cofio 软件 Ltd |
| ipmrsync_mfilter.sys | 281200 | OpenMars 企业 |
| cascade.sys | 281100 | JP 软件 |
| filearchive.sys | 281000 | 代码总结 |
| syscdp.sys | 280900 | 系统确定 AB |
| dpnedriver.sys (x86) | 280850 | HP |
| dpnedriver64.sys (x64) | 280850 | HP |
| hpchgflt.sys | 280800 | HP |
| VirtFile.sys | 280700 | Symantec |
| DeqoCPS.sys | 280600 | Deqo |
| LV_Tracker.sys | 280500 | LiveVault |
| cpbak.sys | 280410 | 检查点软件 |
| tdmonxp.sys | 280400 | TimeData |
| nvfr_cpd | 280310 | Bakbone 软件 inc.保留所有权利。 |
| nvfr_fdd | 280300 | Bakbone 软件 inc.保留所有权利。 |
| Sptbkp.sys | 280290 | Safend |
| accessmonitor.sys | 280280 | Briljant Ekonomisystem |

## <a name="span-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspan260000---269998-fsfilter-content-screener"></a><span id="260000_-_269998__FSFilter_Content_Screener"></span><span id="260000_-_269998__fsfilter_content_screener"></span><span id="260000_-_269998__FSFILTER_CONTENT_SCREENER"></span>260000-269998:FSFilter 内容筛选程序

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| Klshadow.sys | 268300 | Kaspersky 实验室 |
| TN28.sys | 268290 | ID 身份验证技术 |
| PGDriver.sys | 268280 | Avecto Ltd |
| itseczvdb.sys | 268270 | Innotium Inc |
| isarsd.sys | 268260 | ISARS |
| zeoscanner.sys | 268255 | PCKeeper |
| fileHiders.sys | 268250 | PCKeeper |
| cbfltfs4 ObserveIT.sys | 268240 | ObserveIT |
| hipara.sys | 268230 | Allsum LLC |
| AliFileMonitorDriver.sys | 268220 | Alibaba |
| writeGuard.sys | 268210 | TCXA ltd. |
| KKUDKProtectKer.sys | 268200 | Goldmessage 技术共同。 |
| HAWKFIMInt.sys | 268190 | HAWK 网络防御 |
| esaccctl.sys | 268180 | EgoSecure GmbH |
| WSguard.sys | 268170 | 雨刮器软件 UAB |
| Atomizer.sys | 268160 | DragonFlyCodeWorks |
| farwflt.sys | 268150 | Malwarebytes |
| ADSpiderEx2.sys | 268140 | Digitalonnet |
| sdfilter.sys | 268130 | Igor Zorkov |
| Safe.sys | 268120 | rian@alum.mit.edu |
| mydlpdelete scanner.sys | 268110 | Medra Teknoloji |
| mydlpscanner.sys | 268100 | Medra Teknoloji |
| hnpro.sys | 268040 | Solupia |
| DLDriverNetMini.sys | 268030 | DeviceLock Inc |
| ENFFLTDRV.sys | 268020 | Enforcive 系统 |
| imagentpg.sys | 268012 | Infomaximum |
| crocopg.sys | 268010 | Infomaximum |
| sbapifs.sys | 268000 | Sunbelt 软件 |
| H6kernNT.sys | 267920 | H6N 技术 LLC |
| SGKD32。SYS | 267910 | NetSection 安全 |
| IccFilter.sys | 267900 | NEC System 技术 |
| tflbc.sys | 267800 | Tani 电子公司 |
| ArmFlt.sys | 267000 | 破解防病毒软件 |
| WBDrv.sys | 266700 | Axiana LLC |
| DMSamFilter.sys | 266600 | Digimarc corp. |
| mumbl.sys | 266540 | ZenmuTech inc.保留所有权利。 |
| 5nine.cbt.sys | 266100 | 5nine 软件 inc.保留所有权利。 |
| bsfs.sys | 266000 | 快速修复 TechnologiesPvt。 Ltd.  |
| XXRegSFilter.sys | 265910 | Zhe Jiang Xinxin 软件技术。 |
| XXSFilter.sys | 265900 | Zhe Jiang Xinxin 软件技术。 |
| AloahaUSBBlocker.sys | 265800 | Wrocklage Intermedia |
| frxdrv.sys | 265700 | FSLogix inc.保留所有权利。 |
| FolderSecure.sys | 265600 | 最大安全软件 |
| XendowFLTC.sys | 265570 | Credant 技术 |
| RepDac | 265500 | 视觉解决方案 |
| tbbdriver.sys | 265400 | Tedesi |
| spcgrd.sys | 265300 | FUJITSU 广泛解决方案 |
| fdtlock.sys | 265250 | FUJITSU 广泛解决方案和咨询 inc.保留所有权利。 |
| ssfFSC.sys | 265200 | SECUWARE S.L。 |
| GagSecurity.sys | 265120 | 北京 Shu Yan 科学 |
| PrintDriver.sys | 265110 | 北京 Shu Yan 科学 |
| activ.sys | 265100 | Rapidware Pty Ltd |
| avscan.sys | 265010 | Microsoft |
| scanner.sys | 265000 | Microsoft |
| DI_fs.sys | 264910 | 软 SB |
| wgnpos.sys | 264900 | Orchestria |
| odfltr.sys | 264810 | NetClean 技术 |
| ncpafltr.sys | 264800 | NetClean 技术 |
| ct.sys | 264700 | Haute 安全 |
| fvefsmf.sys | 264600 | Fortisphere，inc. |
| block.sys | 264500 | 自治系统限制 |
| csascr.sys | 264400 | Cisco 系统 |
| SymAFR.sys | 264300 | Symantec Corporation |
| cwnep.sys | 264200 | Websense inc.保留所有权利。 |
| spywareremover.sys | 264150 | C Netmedia |
| malwarebot.sys | 264140 | C Netmedia |
| antispywarebot.sys | 264130 | 2Squared inc.保留所有权利。 |
| adwarebot.sys | 264120 | 反间谍软件 LLC |
| antispyware.sys | 264110 | 反间谍软件 LLC |
| spywarebot.sys | 264100 | C Netmedia |
| nomp3.sys | 264000 | Hamish Speirs （专用开发人员） |
| dlfilter.sys | 263900 | Starfield 软件 |
| sifsp.sys | 263800 | Secure Islands Technologies LTD |
| DLFsFlt.sys | 263700 | CenterTools 软件 GmbH |
| SamKeng.sys | 263600 | Syvik 共同，ltd. |
| rml.sys | 263500 | Logis IT 服务 Gmbh |
| vfsmfd.sys | 263410 | Vontu inc.保留所有权利。 |
| vfsmfd.sys | 263400 | Vontu inc.保留所有权利。 |
| acfilter.sys | 263300 | Avalere，inc. |
| psecfilter.sys | 263200 | MDI 实验室，inc. |
| SolRedirect.sys | 263110 | Soliton 系统 |
| solitkm.sys | 263100 | Soliton 系统 |
| ipcfs.sys | 263000 | NetVeda |
| netgateav_access.sys | 262910 | NETGATE 技术。 s.r.o. |
| spyemrg_access.sys | 262900 | NETGATE 技术。 s.r.o. |
| pxrmcet.sys | 262800 | Proxure inc.保留所有权利。 |
| EgisTecFF.sys | 262700 | Egis 技术 inc.保留所有权利。 |
| fgcpac.sys | 262600 | Fortres Grand corp. |
| saappctl.sys | 262510 | SecureAge 技术 |
| sadlp.sys | 262500 | SecureAge 技术 |
| CRExecPrev.sys | 262410 | Cybereason |
| PEG2.sys | 262400 | PE 防护 |
| AdminRunFlt.sys | 262300 | Simon 贾维斯 |
| wvscr.sys | 262200 | 成都 Wei 技术 inc.保留所有权利。 |
| psepfilter.sys | 262100 | 绝对软件 |
| SAMDriver.sys | 262000 | 峰会 IT |
| emrcore.sys | 261920 | Ivanti Inc |
| wire_fsfilter.sys | 261910 | ThreatSpike 实验室 |
| AMFileSystemFilter.sys | 261900 | AppSense Ltd |
| mtflt.sys | 261880 | mTalos inc.保留所有权利。 |
| nxrmflt.sys | 261680 | NextLabs，inc. |
| oc_fsfilter.sys | 261300 | Raiffeisen 银行 Aval |
| hdlpflt.sys | 261200 | McAfee inc.保留所有权利。 |
| CCFFilter.sys | 261160 | Microsoft |
| cbafilt.sys | 261150 | Microsoft |
| SmbBandwidthLimitFilter.sys | 261110 | Microsoft |
| DfsrRo.sys | 261100 | Microsoft |
| DataScrn.sys | 261000 | Microsoft |
| ldusbro.sys | 260900 | LANDesk inc.保留所有权利。 |
| FileScreenFilter.sys | 260800 | Veritas |
| cpAcOnPnP.sys | 260720 | conpal GmbH |
| cpsgfsmf.sys | 260710 | conpal GmbH |
| psmmfilter.sys | 260700 | PolyServe |
| pctefa.sys | 260650 | PC 工具 Pty. Ltd. |
| pctefa64.sys | 260650 | PC 工具 Pty. Ltd. |
| symefasi.sys | 260610 | Symantec Corporation |
| symefa.sys | 260600 | Symantec |
| symefa64.sys | 260600 | Symantec |
| aictracedrv_cs.sys | 260500 | AI 咨询 |
| DWFIxxxx.sys | 260410 | SciencePark Corporation |
| DWFIxxxx.sys | 260400 | SciencePark Corporation |
| DSDriver.sys | 260330 | ManageEngine Zoho Corp |
| mcfltlab.sys | 260320 | 北京 MicroColor |
| FDriver.sys | 260310 | Fox IT |
| iqpk.sys | 260300 | Secure Islands Technologies LTD |
| VHDFlt.sys | 260240 | Dell |
| VHDFlt.sys | 260230 | Dell |
| VHDFlt.sys | 260220 | Dell |
| VHDFlt.sys | 260210 | Dell |

## <a name="span-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspan240000---249999-fsfilter-quota-management"></a><span id="240000_-_249999__FSFilter_Quota_Management"></span><span id="240000_-_249999__fsfilter_quota_management"></span><span id="240000_-_249999__FSFILTER_QUOTA_MANAGEMENT"></span>240000-249999:FSFilter 配额管理

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| ntps_qfs.sys | 245100 | NTP 软件 |
| PSSFsFilter.sys | 245000 | PSS 系统 |
| Sptqmg.sys | 245300 | Safend |
| storqosflt.sys | 244000 | Microsoft |

## <a name="span-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspan220000---229999-fsfilter-system-recovery"></a><span id="220000_-_229999__FSFilter_System_Recovery"></span><span id="220000_-_229999__fsfilter_system_recovery"></span><span id="220000_-_229999__FSFILTER_SYSTEM_RECOVERY"></span>220000-229999:FSFilter 系统恢复

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| file_protector.sys | 227000 | Acronis |
| fbwf.sys | 226000 | Microsoft |
| Klsysrec.sys | 221500 | Kaspersky 实验室 |
| SFDRV。SYS | 221400 | Utixo LLC |
| sp_prot.sys | 221300 | Xacti Corporation |
| nsfilep.sys | 221200 | Netsupport Limited |
| syscow.sys | 221100 | 系统确定 AB |
| fsredir.sys | 221000 | Microsoft |

## <a name="span-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspan200000---209999-fsfilter-cluster-file-system"></a><span id="200000_-_209999__FSFilter_Cluster_File_System"></span><span id="200000_-_209999__fsfilter_cluster_file_system"></span><span id="200000_-_209999__FSFILTER_CLUSTER_FILE_SYSTEM"></span>200000-209999:FSFilter 群集文件系统

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| CVCBT.sys | 203400 | CommVault Systems，inc.保留所有权利。 |
| ResumeKeyFilter.sys | 202000 | Microsoft |

## <a name="span-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspan180000---189999-fsfilter-hsm"></a><span id="180000_-_189999__FSFilter_HSM"></span><span id="180000_-_189999__fsfilter_hsm"></span><span id="180000_-_189999__FSFILTER_HSM"></span>180000-189999:FSFilter HSM

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| wcifs.sys | 189900 | Microsoft |
| prjflt.sys | 189800 | Microsoft |
| gameflt.sys | 189750 | Microsoft |
| nvmsqrd.sys | 188900 | NVIDIA Corporation |
| RsFlt.sys | 187000 | Redstor Limited |
| mnefs.sys | 186800 | Nippon 腔实验室 |
| Svfsf.sys | 186700 | Spharsoft 技术 |
| uVaultFlt.sys | 186650 | DOR |
| syncmf.sys | 186620 | 氧气云 |
| gwmemory.sys | 186600 | Macrotec LLC |
| cteraflt.sys | 186550 | CTERA 网络 ltd. |
| dbx.sys | 186500 | Dropbox inc.保留所有权利。 |
| quaddrasi.sys | 186400 | Quaddra 软件 |
| gdrive.sys | 186300 | Google |
| CoreSyncFilter.sys | 186250 | Adobe Systems inc.保留所有权利。 |
| EaseTag.sys | 186200 | EaseVault Technologies inc. |
| hcminifilter.sys | 186100 | 高兴云 inc.保留所有权利。 |
| PDFsFilter.sys | 186000 | Raxco Sfotware inc.保留所有权利。 |
| camino.sys | 185900 | CaminoSoft Corp |
| C2C_AF1R。SYS | 185810 | C2C 系统 |
| DFdriver.sys | 185800 | DataFirst Corporation |
| amfadrv.sys | 185700 | Quest Software Inc. |
| HSMdriver.sys | 185600 | Wim Vervoorn |
| kdfilter.sys | 185555 | Komprise inc.保留所有权利。 |
| htdafd.sys | 185500 | 桥头软 |
| odphflt.sys | 180455 | Microsoft |
| cldflt.sys | 180451 | Microsoft |
| SymHsm.sys | 185400 | Symantec |
| evmf.sys | 185100 | Symantec |
| otfilter.sys | 185000 | Overtone 软 |
| ithsmdrv.sys | 184900 | IBM |
| MfaFilter.sys | 184800 | Waterford 技术 |
| SonyHsmMinifilter.sys | 184700 | Sony Corporation |
| acahsm.sys | 184600 | 自治 Corporation |
| zlhsm.sys | 184500 | ZL 技术 |
| CFileProtect.sys | 184100 | 浙江安全技术 |
| stc_restore_filter.sys | 184000 | StorageCraft 技术 |
| dvfilter.sys | 183003 | Microsoft |
| Accesstracker.sys | 183002 | Microsoft |
| Changetracker.sys | 183001 | Microsoft |
| Fstier.sys | 183000 | Microsoft |
| hsmcdpflt.sys | 182700 | Metalogix |
| archivmgr.sys | 182690 | Metalogix |
| ntps_oddm.sys | 182600 | NTP 软件 |
| XDFileSys.sys | 182500 | XenData Limited |
| upmjit.sys | 182400 | Citrix Systems |
| AtmosFS.sys | 182310 | EMC Corporation |
| DxSpy.sys | 182300 | EMC 软件 inc.保留所有权利。 |
| car_hsmflt.sys | 182200 | Caringo，inc. |
| BRDriver.sys | 182100 | BitRaider |
| BRDriver64.sys | 182100 | BitRaider |
| autnhsm.sys | 182000 | 自治 Corporation |
| cthsmflt.sys | 181970 | ComTrade |
| NxMini.sys | 181900 | NEXSAN |
| neuflt.sys | 181818 | NeuShield |
| npfdaflt.sys | 181800 | Mimosa Systems Inc |
| AppStream.sys | 181700 | 应用程序流，inc. |
| HPEDpHsmX64.sys | 181620 | Hewlett-Packard Co.， |
| HPArcHsmX64.sys | 181610 | Hewlett-Packard Co.， |
| hphsmflt.sys | 181600 | Hewlett-Packard Co.， |
| cparchsm.sys | 181610 | Micro 焦点 |
| RepHsm.sys | 181500 | Double-take 软件，inc.保留所有权利 |
| RepSIS.sys | 181490 | Double-take 软件 |
| SquashCompressionFsFilter.sys | 181410 | Squash 压缩 |
| GXHSM.sys | 181400 | Commvault 系统，Inc |
| EdsiHsm.sys | 181300 | 企业数据的解决方案，inc. |
| BkfMap.sys | 181200 | 数据存储组 |
| hsmfilter.sys | 181100 | GRAU 数据存储可用性组 |
| mwilcflt.sys | 181020 | 月球漫步的例子通用的 P L |
| mwilsflt.sys | 181010 | 月球漫步的例子通用的 P L |
| mwidmflt.sys | 181000 | 月球漫步的例子通用的 P L |
| HcpAwfs.sys | 181960 | 人： Hitachi 数据系统 |
| sdrefltr.sys | 180950 | 人： Hitachi 数据系统 |
| fltasm.sys | 180900 | 全局 360 |
| cnet_hsm.sys | 180850 | Carroll Net inc.保留所有权利。 |
| pntvolflt.sys | 180800 | 点软件和系统 |
| appxstrm.sys | 180710 | Microsoft |
| wimmount.sys | 180700 | Microsoft |
| hsmflt.sys | 180600 | Microsoft |
| dfsrflt.sys | 180500 | Microsoft |
| StorageSyncGuard.sys | 180465 | Microsoft |
| StorageSync.sys | 180460 | Microsoft |
| dedup.sys | 180450 | Microsoft |
| dfmflt.sys | 180410 | Microsoft |
| sis.sys | 180400 | Microsoft |
| rbt_wfd.sys | 180300 | Riverbed 技术，Inc |

## <a name="span-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspan170000---174999-fsfilter-imaging-ex-zip"></a><span id="170000_-_174999__*FSFilter_Imaging_(ex:_.ZIP)"></span><span id="170000_-_174999__*fsfilter_imaging_(ex:_.zip)"></span><span id="170000_-_174999__*FSFILTER_IMAGING_(EX:_.ZIP)"></span>170000-174999: * FSFilter 映像 (例如:。ZIP)

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| pfmfs_ 批处理。sys | 172100 | Pismo Technic Inc |
| virtual_file.sys | 172000 | Acronis |
| wimFltr.sys | 170500 | Microsoft |

## <a name="span-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspan160000---169999-fsfilter-compression"></a><span id="160000_-_169999__FSFilter_Compression"></span><span id="160000_-_169999__fsfilter_compression"></span><span id="160000_-_169999__FSFILTER_COMPRESSION"></span>160000-169999:FSFilter 压缩

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| CmgFFC.sys | 166000 | Credant 技术 |
| compress.sys | 165000 | Microsoft |
| cmpflt.sys | 162000 | Microsoft |
| IridiumIO.sys | 161700 | Confio |
| logcompressor.sys | 161600 | VelociSQL inc.保留所有权利。 |
| GcfFilter.sys | 161500 | GemacmbH |
| ssddoubler.sys | 161400 | 思南 Karaca |
| Sptcmp.sys | 161300 | Safend |
| wimfsf.sys | 161000 | Microsoft |
| GEFCMP.sys | 160100 | Symantec |

## <a name="span-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspan140000---149999-fsfilter-encryption"></a><span id="140000_-_149999__FSFilter_Encryption"></span><span id="140000_-_149999__fsfilter_encryption"></span><span id="140000_-_149999__FSFILTER_ENCRYPTION"></span>140000-149999:FSFilter 加密

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| FJSeparettiFilterRamMon.sys | 149100 | FUJITSU LIMITED |
| psatfilter.sys | 149050 | ProYuga |
| RdFilter.sys | 149040 | CyberEye 研究实验室 |
| gisfile_decryption.sys | 149030 | 通信 U 中国 |
| TIFSFilter.sys | 149020 | SG Corporation |
| OsrDt2.sys | 149010 | 信息安全 Corp |
| EasyKryptMF.sys | 149000 | SoftKrypt LLC |
| padlock.sys | 148910 | IntSoft inc.保留所有权利。 |
| ffecore.sys | 148900 | Winmagic |
| fangcloud.sys | 148860 | 杭州 Yifangyun |
| klvfs.sys | 148810 | Kaspersky 实验室 |
| Klfle.sys | 148800 | Kaspersky 实验室 |
| ISFP.sys | 148701 | 安装 ALPS 系统集成中 |
| ISIRM.sys | 148700 | 安装 ALPS 系统集成 CO。 |
| ASUSSecDrive.sys | 148650 | ASUS |
| ABFilterDriver.sys | 148640 | AlertBoot |
| QDocumentFSF.sys | 148630 | BicDroid inc.保留所有权利。 |
| bfusbenc.sys | 148620 | bitFence inc.保留所有权利。 |
| sztgbfsf.sys | 148610 | SaferZone Co. |
| mwIPSDFilter.sys | 148600 | Egis 技术 inc.保留所有权利。 |
| csccvdrv.sys | 148500 | 计算机科学 Corporation |
| aefs.sys | 148400 | Angelltech Corporation Xi'an |
| VTEFsFlt.sys | 148374 | EsComputer Corp |
| IWCSEFlt.sys | 148300 | InfoWatch |
| GDDmk.sys | 148250 | G 数据 Software AG |
| clcxcore.sys | 148210 | 漂亮 Solutions Inc. |
| OrisLPDrv.sys | 148200 | CGS 发布技术 |
| nlemsys.sys | 148100 | NETLIB |
| prvflder.sys | 148000 | Microsoft |
| ssefs.sys | 147900 | SecuLution GmbH |
| SePSed.sys | 147800 | 嗡嗡头，inc. |
| dlmfencx.sys | 147700 | 数据加密 Ltd |
| SkyDEnc.sys | 147620 | 天空共同 Ltd |
| psgcrypt.sys | 147610 | Yokogawa R & L Corp |
| bbfsflt.sys | 147600 | Bloombase |
| qx10efs.sys | 147500 | Quixxant |
| MEfefs.sys | 147400 | Eruces inc.保留所有权利。 |
| medlpflt.sys | 147310 | 检查点软件 Technologies Ltd |
| dsfa.sys | 147308 | 检查点软件 Technologies Ltd |
| Snicrpt.sys | 147300 | Systemneeds，Inc |
| iCrypt.sys | 147200 | I/O 数据设备，INC. |
| xdrmflt.sys | 147100 | bluefinsystems |
| dyFsFilter.sys | 147000 | Scrypto 媒体 |
| thinairwin.sys | 146960 | 精简空气 Inc" |
| UcaDataMgr.sys | 146950 | AppSense Ltd |
| zesocc.sys | 146900 | Novell |
| mfprom.sys | 146800 | McAfee Inc |
| MfeEEFF.sys | 146790 | McAfee inc.保留所有权利。 |
| intefs.sys | 146700 | TianYu 软件 |
| leofs.sys | 146600 | Leotech |
| autocryptater.sys | 146500 | Richard Hagen |
| WavxDMgr.sys | 146400 | Scott Cochrane |
| eedmkxp32.sys | 146300 | Entrust |
| SbCe.sys | 146200 | 安全引导 |
| iSharedFsFilter | 146100 | Packeteer Inc |
| dlrmenc.sys | 146010 | DESlock |
| dlmfenc.sys | 146000 | DESlock |
| aksdf.sys | 145900 | 限于 Aladdin 知识系统 |
| DDSFilter.sys | 145800 | WuHan Forworld 软件 |
| SecureShield.sys | 145700 | HMI |
| AifaFE.sys | 145600 | Alfa |
| GBFsMf.sys | 145500 | GreenBorder |
| jmefs.sys | 145400 | 上海发电 |
| emugufs.sys | 145333 | Emugu 安全 FS |
| VFDriver.sys | 145300 | R 系统 |
| IntelDG.sys | 145250 | Intel Corporation |
| DPMEncrypt.sys | 145240 | Randtronics Pty |
| EVSDecrypt64.sys | 145230 | Fortium Technologies Ltd |
| skycryptorencfs.sys | 145220 | Onecryptor CJSC。 |
| AisLeg.sys | 145210 | 有保证的信息安全 |
| windtalk.sys | 145200 | Hyland 软件 |
| TeamCryptor.sys | 145190 | iTwin Pte。 Ltd. |
| CVDLP.sys | 145180 | CommVault Systems，inc.保留所有权利。 |
| 5nine.encryptor.sys | 145170 | 5nine 软件 inc.保留所有权利。 |
| ctpfile.sys | 145160 | 北京 Wondersoft 技术 Co. |
| DPDrv.sys | 145150 | IBM 日本 |
| tsdlp.sys | 145140 | Forware |
| KCDriver.sys | 145130 | Tallegra Ltd |
| CmgFFE.sys | 145120 | Credant 技术 |
| fgcenc.sys | 145110 | Fortres Grand corp. |
| sview.sys | 145100 | Cinea |
| TalkeyFilterDriver.sys | 145040 | myTALKEY s.r.o. |
| FedsFilterDriver.sys | 145010 | 物理制作 Corp |
| stocc.sys | 145000 | Senforce 技术 |
| SnEfs.sys | 144900 | Informzaschita |
| ewSecureDox | 144800 | Echoworx Corporation |
| osrdmk.sys | 144700 | OSR 打开系统资源，inc. |
| uldcr.sys | 144600 | NCR 财务解决方案 |
| Tkefsxp.sys-32 位 | 144500 | INCA Internet Co.，Ltd |
| Tkefsxp64.sys-64 位 | 144500 | INCA Internet Co.，Ltd |
| NmlAccf.sys | 144400 | NEC 系统技术，ltd. |
| SolCrypt.sys | 144300 | Soliton 系统 K.K. |
| IngDmk.sys | 144200 | Ingrian 网络，inc. |
| llenc.sys | 144100 | SecureAxis 软件 |
| SecureData.sys | 144030 | SecureAge 技术 |
| lockcube.sys | 144020 | SecureAge 技术 Pte Ltd |
| sdmedia.sys | 144010 | SecureAge 技术 |
| mysdrive.sys | 144000 | SecureAge 技术 |
| FileArmor.sys | 143900 | 移动破解 |
| VSTXEncr.sys | 143800 | 通过技术，inc. |
| dgdmk.sys | 143700 | Verdasys inc.保留所有权利。 |
| shandy.sys | 143600 | Safend ltd. |
| C2knet.sys | 143520 | Secuware |
| C2kdef.sys | 143510 | Secuware |
| ssfFS.sys | 143500 | SECUWARE S.L。 |
| PISRFE.sys | 143400 | Jilin 大学 IT Co. |
| bapfecre.sys | 143300 | BitArmor 系统，Inc |
| KPSD.sys | 143200 | cihosoft |
| Fcfileio.sys | 143100 | Brainzsquare，Co.Ltd. |
| cpdrm.sys | 143000 | Pikewerks |
| vmfiltr.sys | 142900 | Vormetric Inc |
| VFSEnc.sys | 142811 | Symantec |
| pgpfs.sys | 142810 | Symantec |
| fencry.sys | 142800 | Symantec |
| TmFileEncDmk.sys | 142700 | Trend Micro Inc |
| cpefs.sys | 142600 | 加密 Pro |
| dekfs.sys | 142500 | KasherLab co.ltd |
| qlockfilter.sys | 142400 | Binqsoft inc.保留所有权利。 |
| RRFilterDriverStack_d3.sys | 142300 | 合理的保留期 |
| cve.sys | 142200 | 绝对软件 corp. |
| spcflt.sys | 142100 | FUJITSU BSC inc.保留所有权利。 |
| ldsecusb.sys | 142000 | LANDesk inc.保留所有权利。 |
| fencr.sys | 141900 | SODATSW spol。 s.r.o. |
| RubiFlt.sys | 141800 | 人： Hitachi |
| mfild.sys | 141660 | Penta 安全系统 |
| cbfsfilter2017.sys | 141635 | 自动 Inc |
| cbfsfilter2017.sys | 141634 | 自动 Inc |
| cbfsfilter2017.sys | 141633 | 自动 Inc |
| cbfsfilter2017.sys | 141632 | 自动 Inc |
| cbfsfilter2017.sys | 141631 | 自动 Inc |
| cbfsfilter2017.sys | 141630 | 自动 Inc |
| TypeSquare.sys | 141620 | Morisawa inc。 |
| xbdocfilter.sys | 141610 | Zrxb |
| EVSDecrypt32.sys | 141600 | Fortium Technologies Ltd |
| EVSDecrypt64.sys | 141600 | Fortium Technologies Ltd |
| EVSDecryptia64.sys | 141600 | Fortium Technologies Ltd |
| SophosDt2.sys | 141510 | Sophos Plc |
| afdriver.sys | 141500 | ATUS 技术 LLC |
| TrivalentFSFltr.sys | 141430 | 网络依赖 |
| CmdMnEfs.sys | 141420 | Comodo 安全 |
| DWENxxxx.sys | 141410 | SciencePark Corporation |
| DWENxxxx.sys | 141400 | SciencePark Corporation |
| hdFileSentryDrv32.sys | 141300 | Heilig 防御 |
| hdFileSentryDrv64.sys | 141300 | Heilig 防御 |
| CovertxFilter.sys | 141240 | Micro 焦点 |
| cplcdt2.sys | 141230 | conpal GmbH |
| asCryptoFilter.sys | 141220 | 应用的安全 GmbH |
| NetCryptKR.sys | 141210 | NetCrypt Pty Ltd |
| BHFilter.sys | 141200 | 鱼叉解决方案 |
| Filecrypt.sys | 141100 | Microsoft |
| encrypt.sys | 141010 | Microsoft |
| swapBuffers.sys | 141000 | Microsoft |

## <a name="span-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspan130000---139999-fsfilter-virtualization"></a><span id="130000_-_139999__FSFilter_Virtualization"></span><span id="130000_-_139999__fsfilter_virtualization"></span><span id="130000_-_139999__FSFILTER_VIRTUALIZATION"></span>130000-139999:FSFilter 虚拟化

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| Klvirt.sys | 138100 | Kaspersky 实验室 |
| VMagic.sys | 138050 | AI 咨询 |
| GetSAS.sys | 138040 | SAS Institute Inc |
| rqtNos.sys | 138030 | ReaQta ltd. |
| HIPS64.sys | 138020 | Recrypt LLC |
| frxdrv.sys | 138010 | FSLogix inc.保留所有权利。 |
| vzdrv.sys | 138000 | Altiris |
| sffsg.sys | 137990 | 海星存储 Corp |
| AppStream.sys | 137920 | Symantec Corporation |
| Rasm.sys | 137915 | OpDesk Inc |
| boxifier.sys | 137910 | Kenubi |
| xorw.sys | 137900 | CA (XOsoft) |
| ctlua.sys | 137800 | SurfRight B.V. |
| fgccow.sys | 137700 | Fortres Grand corp. |
| aswSnx.sys | 137600 | ALWIL 软件 |
| AppIsoFltr.sys | 137500 | 内核驱动程序 |
| ptcvfsd.sys | 137400 | PTC |
| BDSandBox.sys | 137300 | BitDefender SRL |
| sxfpss virt.sys | 137200 | Skanix AS |
| DKRtWrt.sys | 137100 | 为 diskeeper Corporation |
| ivm.sys | 137000 | RingCube 技术 |
| ivm.sys | 136990 | Citrix Systems |
| dtiof.sys | 136900 | Instavia 软件 inc.保留所有权利。 |
| NxTopCP.sys | 136800 | 虚拟计算机的消息 inc.保留所有权利。 |
| svdriver.sys | 136700 | VMware，inc. |
| unifltr.sys | 136600 | Unidesk |
| unidrive.sys （重命名） | 136600 | Unidesk |
| unirsd.sys | 136600 | Unidesk |
| ive.sys | 136500 | TrendMicro inc.保留所有权利。 |
| odamf.sys | 136450 | Sony Corporation |
| SrMxfMf.sys | 136440 | Sony Corporation |
| pszmf.sys | 136430 | Sony Corporation |
| sxsudfmf.sys | 136410 | Sony Corporation |
| vfammf.sys | 136400 | Sony Corporation |
| VHDFlt.sys | 136240 | Dell |
| VHDFlt.sys | 136230 | Dell |
| VHDFlt.sys | 136220 | Dell |
| VHDFlt.sys | 136210 | Dell |
| ncfsfltr.sys | 136200 | NComputing inc.保留所有权利。 |
| cmdguard.sys | 136100 | COMODO 安全解决方案 Inc |
| hpfsredir.sys | 136000 | HP |
| svhdxflt.sys | 135100 | Microsoft |
| luafv.sys | 135000 | Microsoft |
| ivm.sys | 134000 | RingCube 技术 |
| ivm.sys | 133990 | Citrix Systems |
| frxdrvvt.sys | 132700 | FSLogix inc.保留所有权利。 |
| pfmfs_ 批处理。sys | 132600 | Pismo Technic inc.保留所有权利。 |
| Stcvhdmf.sys | 132600 | StorageCraft 技术 Corp |
| appdrv01.sys | 132500 | 保护技术 |
| virtual_file.sys | 132400 | Acronis |
| pdiFsFilter.sys | 132300 | Proximal 数据 inc.保留所有权利。 |
| avgvtx86.sys | 132200 | AVG 技术 CZ |
| avgvtx64.sys | 132200 | AVG 技术 CZ |
| DataNet_Driver.sys | 132100 | AppSense Ltd |
| EgenPage.sys | 132000 | Egenera，inc. |
| unidrive.sys 旧 | 131900 | Unidesk |
| ivm.sys.old | 131800 | RingCube 技术 |
| XiaobaiFsR.sys | 131710 | 深圳 UNNOO LTD |
| XiaobaiFs.sys | 131700 | 深圳 UNNOO LTD |
| iotfsflt.sys | 131600 | IO 涡轮机 Inc |
| mhpvfs.sys | 131500 | Wunix Limited |
| svdriver.sys | 131400 | SnapVolumes inc.保留所有权利。 |
| Sptvrt.sys | 131300 | Safend |
| antirswf.sys | 131210 | Panzor 网络安全 |
| aicvirt.sys | 131200 | AI 咨询 |
| sfo.sys | 130100 | Microsoft |
| DeVolume.sys | 130000 | Microsoft |

## <a name="span-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspan120000---129999-fsfilter-physical-quota-management"></a><span id="120000_-_129999__FSFilter_Physical_Quota_management"></span><span id="120000_-_129999__fsfilter_physical_quota_management"></span><span id="120000_-_129999__FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>120000-129999:FSFilter 物理配额管理

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| quota.sys | 125000 | Microsoft |
| qafilter.sys | 124000 | Veritas |
| DroboFlt.sys | 123900 | 数据机器人 |

## <a name="span-id100000-109999fsfilteropenfilespanspan-id100000-109999fsfilteropenfilespanspan-id100000-109999fsfilteropenfilespan100000---109999-fsfilter-open-file"></a><span id="100000_-_109999__FSFilter_Open_File"></span><span id="100000_-_109999__fsfilter_open_file"></span><span id="100000_-_109999__FSFILTER_OPEN_FILE"></span>100000-109999:FSFilter 打开文件

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| insyncmf.sys | 105000 | InSync |
| SPILock8.sys | 100900 | 软件需要 inc.保留所有权利。 |
| Klbackupflt.sys | 100800 | Kaspersky |
| repkap | 100700 | 视觉解决方案 |
| symrg.sys | 100600 | Symantec |
| adsfilter.sys | 100500 | PolyServ |

## <a name="span-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspan80000---89999-fsfilter-security-enhancer"></a><span id="80000_-_89999__FSFilter_Security_Enhancer"></span><span id="80000_-_89999__fsfilter_security_enhancer"></span><span id="80000_-_89999__FSFILTER_SECURITY_ENHANCER"></span>80000-89999:FSFilter 安全不得不

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| psprotf.sys | 88210 | Panzor 网络安全 |
| DPMACL.sys | 88100 | Randtronics Pty |
| dsbwnck.sys | 88000 | 简单的解决方案 inc.保留所有权利。 |
| cbfsfilter2017.sys | 87910 | 自动化 |
| cbfsfilter2017.sys | 87909 | 自动 Inc |
| cbfsfilter2017.sys | 87908 | 自动 Inc |
| cbfsfilter2017.sys | 87907 | 自动 Inc |
| cbfsfilter2017.sys | 87906 | 自动 Inc |
| cbfsfilter2017.sys | 87905 | 自动 Inc |
| cbfsfilter2017.sys | 87904 | 自动 Inc |
| cbfsfilter2017.sys | 87903 | 自动 Inc |
| cbfsfilter2017.sys | 87902 | 自动 Inc |
| cbfsfilter2017.sys | 87901 | 自动 Inc |
| cbfsfilter2017.sys | 87900 | 自动 Inc |
| rsbfsfilter.sys | 87800 | Corel Corporation |
| hsmltflt.sys | 87720 | 人： Hitachi Solutions |
| hssfflt.sys | 87710 | 人： Hitachi Solutions |
| acmnflt.sys | 87708 | 人： Hitachi Solutions |
| ACSKFFD.sys | 87700 | 人： Hitachi Solutions |
| MyDLPMF.sys | 87600 | Comodo Group 有限公司 |
| ScuaRaw.sys | 87500 | SCUA Seguran&#231;da 缓慢&#231;&#227;o |
| HDSFilter.sys | 87400 | NeoAutus 自动化系统 |
| ikfsmflt.sys | 87300 | IronKey inc.保留所有权利。 |
| Klsec.sys | 87200 | Kaspersky 实验室 |
| XtimUSBFsFilterDrv.sys | 87190 | 大连 CP SDT Ltd |
| RGFLT_FM.sys | 87180 | Hauri.inc |
| flockflt.sys | 87170 | Ahranta inc.保留所有权利。 |
| ZdCore.sys | 87160 | Zends 技术解决方案 |
| dcrypt.sys | 87150 | ReactOS Foundation |
| hpradeo.sys | 87140 | Pradeo |
| SDFSAGDRV。SYS | 87130 | 安装 ALPS 系统集成 CO。 |
| SDFSDEVFDRV。SYS | 87120 | 安装 ALPS 系统集成 CO。 |
| SDIFSFDRV。SYS | 87110 | 安装 ALPS 系统集成 CO。 |
| SDFSFDRV。SYS | 87100 | 安装 ALPS 系统集成 CO。 |
| CModule.sys | 87070 | 浙江安全技术 |
| HHRRPH.sys | 87010 | 软件 H + H GmbH |
| HHVolFltr.sys | 87000 | 软件 H + H GmbH |
| SbieDrv.sys | 86900 | Sandboxie L.T.D |
| assetpro.sys | 86800 | pyaprotect&#x2024;com |
| dlp.sys | 86700 | Tellus 软件 AS |
| eps.sys | 86600 | Lumension 安全 |
| RapportPG64.sys | 86500 | Trusteer |
| amminifilter.sys | 86400 | AppSense |
| Sniflt.sys | 86300 | Systemneeds，Inc |
| SecFile.sys | 86200 | 安全设计 Inc. |
| philly.sys | 86110 | triCerat inc.保留所有权利。 |
| reggy.sys | 86100 | triCerat inc.保留所有权利。 |
| cygfilt.sys | 86000 | Livegrid 合并 |
| prelaunch.sys | 85900 | D3L |
| csareg.sys | 85810 | Cisco 系统 |
| csaenh.sys | 85800 | Cisco 系统 |
| asEpsDrv.sys | 85750 | ASHINI 有限公司 |
| CIDACL.sys | 85700 | GE 航空 (数字系统 Germantown) |
| CVDLP.sys | 85610 | CommVault Systems，inc.保留所有权利。 |
| QGPEFlt.sys | 85600 | Quest Software |
| Drveng.sys | 85500 | CA |
| vracfil2.sys | 85400 | HAURI |
| TFsDisk.sys | 85300 | Teruten |
| rcMiniDrv.sys | 85200 | REDGATE CO.，LTD. |
| SnMc5xx.sys | 85100 | Informzaschita |
| FSPFltd.sys | 85010 | Alfa |
| AifaFFP.sys | 85000 | Alfa |
| EsAccCtlFE.sys | 84901 | EgoSecure GmbH |
| DpAccCtl.sys | 84900 | Softbroker GmbH |
| privman.sys | 84800 | BeyondTrust |
| eumntvol.sys | 84700 | Eugrid Inc |
| SoloEncFilter.sys | 84600 | Soliton 系统 |
| sbfilter.sys | 84500 | UC4 软件 |
| cposfw.sys | 84450 | 检查点软件 Technologies Ltd |
| vsdatant.sys | 84400 | 区域实验室 LLC |
| SePnet.sys | 84350 | 嗡嗡头，inc. |
| SePuld.sys | 84340 | 嗡嗡头，inc. |
| SePpld.sys | 84330 | 嗡嗡头，inc. |
| SePfsd.sys | 84320 | 嗡嗡头，inc. |
| SePwld.sys | 84310 | 嗡嗡头，inc. |
| SePprd.sys | 84300 | 嗡嗡头，inc. |
| InPFlter.sys | 84200 | 嗡嗡头，inc. |
| CProCtrl.sys | 84100 | 加密 Pro |
| spyshelter.sys | 84000 | Datpol |
| clpinspprot.sys | 83900 | 信息技术公司 ltd. |
| uvmfsflt.sys | 83376 | NEC Corporation  |
| ProtectIt.sys | 82373 | TeraByte inc.保留所有权利。 |
| dguard.sys | 82300 | Dmitry Varshavsky |
| NSUSBStorageFilter.sys | 82200 | NetSupport Ltd |
| RMSEFFMV。SYS | 82100 | CJSC Returnil 软件 |
| BoksFLAC.sys | 82000 | Fox 技术 |
| cpAcOnPnP.sys | 81910 | conpal GmbH |
| cpsgfsmf.sys | 81900 | conpal GmbH |
| ndevsec.sys | 81800 | Norman ASA |
| ViewIntus_RTDG.sys | 81700 | Pentego Technologies Ltd |
| airlock.sys | 81630 | 太空飞船数字 Pty Ltd |
| zam.sys | 81620 |  |
| ANXfsm.sys | 81610 | Arcdo |
| CDrSDFlt.sys | 81600 | Arcdo |
| crnselfdefence32.sys | 81500 | Coranti inc.保留所有权利。 |
| crnselfdefence64.sys | 81500 | Coranti inc.保留所有权利。 |
| zlock_drv.sys | 81400 | SecurIT |
| f101fs.sys | 81300 | Fortres Grand corp. |
| sysgar.sys | 81200 | 核心数据恢复 |
| EmbargoM.sys | 81100 | 试一下 ScriptLogic |
| ngssdef.sys | 81050 | Wontok Inc |
| ssb.sys | 81041 | Wontok Inc |
| regflt.sys | 81040 | Wontok Inc |
| fsds2a.sys | 81000 | Splitstreem Ltd |
| csacentr.sys | 80900 | Cisco 系统 |
| ScvFLT50.sys | 80850 | Secuve Ltd |
| paritydriver.sys | 80800 | Bit9，inc. |
| nkfsprot.sys | 80710 | Konneka |
| nkprot.sys | 80700 | KONNEKA 信息技术 |
| acpadlock.sys | 80691 | IntSoft Co |
| ksmf.sys | 80690 | IntSoft Co |
| im.sys | 80680 | CrowdStrike |
| SophosED.sys | 80670 | Sophos |
| jazzfile.sys | 80660 | 爵士乐网络 |
| SMXFs.sys | 80500 | OSR |

## <a name="span-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspan60000---69999-fsfilter-copy-protection"></a><span id="60000_-_69999__FSFilter_Copy_Protection"></span><span id="60000_-_69999__fsfilter_copy_protection"></span><span id="60000_-_69999__FSFILTER_COPY_PROTECTION"></span>60000-69999:FSFilter 复制保护

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| d3clock.sys | 67000 | D3CRYPT3D LLC |
| cbfltfs4.sys | 66500 | I3D 技术 Inc |
| CkProcess.sys | 66100 | KASHU 系统设计 INC.保留所有权利。 |
| dlmfprot.sys | 66000 | 数据加密 Sys |
| baprtsef.sys | 65700 | BitArmor 系统，Inc |
| sxfpss.sys | 65600 | Skanix AS |
| rgasdev.sys | 65500 | Macrovision |
| SkyFPDrv.sys | 65410 | 天空有限公司 |
| SkyLWP.sys | 65400 | 天空有限公司 |
| SnEraser.sys | 65300 | Informzaschita |
| vfilter.sys | 65200 | RSJ 软件 GmbH |
| COGOFlt32.sys | 65100 | Fortium Technologies Ltd |
| COGOFlt64.sys | 65100 | Fortium Technologies Ltd |
| COGOFLTia64.sys | 65100 | Fortium Technologies Ltd |
| scrubber.sys | 65000 | Microsoft |
| BRDriver.sys | 64000 | BitRaider LLC |
| BRDriver64.sys | 64000 | BitRaider LLC |
| X7Ex.sys | 62500 | Exent Technologies Ltd |
| LibertyFSF.sys | 62300 | Bayalink 解决方案 Co |
| axfsdrv2.sys | 62100 | Axence 软件 inc.保留所有权利。 |
| sds.sys | 62000 | 出口软件 |
| TotalSystemAuditor.sys | 61600 | ANRC LLC |
| MBAMApiary.sys | 61500 | Malwarebytes corp. |
| WA_FSW.sys | 61400 | Programas Administraci&#243;n y Mejoramiento |
| ViewIntus_RTAS | 61300 | Pentego 技术 |
| tffac.sys | 61200 | Toshiba Corporation |
| tccp.sys | 61100 | TrusCont Ltd |
| KomFS.sys | 61000 | KOM 网络 |

## <a name="span-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspan40000---49999-fsfilter-bottom"></a><span id="40000_-_49999__FSFilter_Bottom"></span><span id="40000_-_49999__fsfilter_bottom"></span><span id="40000_-_49999__FSFILTER_BOTTOM"></span>40000-49999:FSFilter 底部

| 微筛选器                  | 海拔高度 | 公司                                 |
------------------------------|----------|-----------------------------------------|
| RMPFileMounter.sys | 48000 | ManageEngine Zoho |
| cbfsfilter2017.sys | 47400 | 12d 式开发相配合 |
| pfmfs_ 批处理。sys | 47300 | Pismo Technic inc.保留所有权利。 |
| DLDriverMiniFlt.sys | 47200 | DeviceLock Inc |
| hsmltlib.sys | 47110 | 人： Hitachi Solutions |
| hskdlib.sys | 47100 | 人： Hitachi Solutions |
| acmnlib.sys | 47090 | 人： Hitachi Solutions |
| aictracedrv_b.sys | 47000 | AI 咨询 |
| hhdcfltr.sys | 46900 | Seagate 技术 |
| Npsvctrig.sys | 46000 | Microsoft |
| klvfs.sys | 44900 | Kaspersky 实验室 |
| Klbackupflt.sys | 44890 | Kaspersky 实验室 |
| rsfxdrv.sys | 41000 | Microsoft |
| defilter.sys | 40900 | Microsoft |
| AppVVemgr.sys | 40800 | Microsoft |
| wofadk.sys | 40730 | Microsoft |
| wof.sys | 40700 | Microsoft |
| fileinfo | 40500 | Microsoft |
| WinSetupBoot.sys | 40400 | Microsoft |

## <a name="span-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspan20000---29999-fsfilter-system"></a><span id="20000_-_29999__FSFilter_System"></span><span id="20000_-_29999__fsfilter_system"></span><span id="20000_-_29999__FSFILTER_SYSTEM"></span>20000-29999:FSFilter 系统

无。
