---
title: 分配的等级
description: 分配的等级
ms.assetid: EC1993FB-5219-4C0C-A76A-05937A461C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd0b26a0114a0a2e60565ccdc4f0dc04c073105
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568408"
---
# <a name="allocated-altitudes"></a>分配的等级


文件系统微筛选器驱动程序开发到筛选器管理器模型必须具有名为海拔高度，用于定义其位置相对于存在于文件系统堆栈中其他微筛选器的唯一标识符。 由 Microsoft 根据微筛选器要求和加载顺序组分配海拔微筛选器的地区。

为每个以下的加载顺序组列出了当前的海拔高度分配。

## <a name="span-id420000-429999filterspanspan-id420000-429999filterspanspan-id420000-429999filterspan420000---429999-filter"></a><span id="420000_-_429999__Filter"></span><span id="420000_-_429999__filter"></span><span id="420000_-_429999__FILTER"></span>420000 - 429999:Filter


| 微筛选器   | 海拔高度 | 公司   |
|--------------|----------|-----------|
| ntoskrnl.exe | 425500   | Microsoft |
| ntoskrnl.exe | 425000   | Microsoft |



## <a name="span-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspan400000---409999-fsfilter-top"></a><span id="400000_-_409999__FSFilter_Top"></span><span id="400000_-_409999__fsfilter_top"></span><span id="400000_-_409999__FSFILTER_TOP"></span>400000 - 409999:FSFilter 顶部


| 微筛选器                    | 海拔高度 | 公司                  |
|-------------------------------|----------|--------------------------|
| wcnfs.sys                     | 409900   | Microsoft                |
| iorate.sys                    | 409010   | Microsoft                |
| ioqos.sys                     | 409000   | Microsoft                |
| fsdepends.sys                 | 407000   | Microsoft                |
| sftredir.sys                  | 406000   | Microsoft                |
| dfs.sys                       | 405000   | Microsoft                |
| csvnsflt.sys                  | 404900   | Microsoft                |
| csvflt.sys                    | 404800   | Microsoft                |
| Microsoft.Uev.AgentDriver.sys | 404710   | Microsoft                |
| AppvVfs.sys                   | 404700   | Microsoft                |
| eaw.sys                       | 401900   | Raytheon 网络解决方案 |
| TVFsfilter.sys                | 401800   | TrustView                |
| KKDiskProtecter.sys           | 401700   | Goldmsg                  |
| AgentComm.sys                 | 401600   | 开发持有锁        |
| rvsavd.sys                    | 401500   | CJSC Returnil 软件   |
| dgdmk.sys                     | 401400   | Verdasys Inc.            |
| tusbstorfilt.sys              | 401300   | SimplyCore LLC           |
| pcgenfam.sys                  | 401200   | Soluto                   |
| atrsdfw.sys                   | 401100   | Altiris                  |
| tpfilter.sys                  | 401000   | RedPhone 安全        |
| mbamwatchdog.sys              | 400900   | Malwarebytes Corporation |
| edevmon.sys                   | 400800   | 重置                     |
| vmwflstor.sys                 | 400700   | VMware, Inc.             |
| TsQBDrv.sys                   | 400600   | 腾讯技术       |



## <a name="span-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspan-360000---389999-fsfilter-activity-monitor"></a><span id="_360000_-_389999__FSFilter_Activity_Monitor"></span><span id="_360000_-_389999__fsfilter_activity_monitor"></span><span id="_360000_-_389999__FSFILTER_ACTIVITY_MONITOR"></span> 360000 - 389999:FSFilter 活动监视器


| 微筛选器                       | 海拔高度 | 公司                                                |
|----------------------------------|----------|--------------------------------------------------------|
| drbdlock.sys                     | 389090   | Man 技术 Inc                                     |
| hsmltmon.sys                     | 389080   | 人： Hitachi Solutions                                      |
| AternityRegistryHook.sys         | 389070   | Aternity Ltd                                           | 
| CSBFilter.sys                    | 389060   | Carbonite Inc                                          |
| ChemometecFilter.sys             | 389050   | ChemoMetec                                             | 
| SentinelMonitor.sys              | 389040   | SentinelOne                                            |
| DhWatchdog.sys                   | 389030   | Microsoft                                              |
| edrsensor.sys                    | 389025   | Bitdefender SRL                                        |
| NpEtw.sys                        | 389020   | Koby Kahane                                            |
| OczMiniFilter.sys                | 389010   | OCZ 存储                                            |
| ielcp.sys                        | 389004   | Intel Corporation                                      |
| IESlp.sys                        | 389002   | Intel Corporation                                      |
| IntelCAS.sys                     | 389000   | Intel Corporation                                      |
| boxifier.sys                     | 388990   | Kenubi                                                 |
| SamsungRapidFSFltr.sys           | 388980   | NVELO                                                  |
| drsfile.sys                      | 388970   | MRY Inc.                                               |
| CrUnCopy.sys                     | 388964   | Shenzhen CloudRiver                                    |
| aictracedrv\_am.sys              | 388960   | AI 咨询                                          |
| fiopolicyfilter.sys              | 388954   | SanDisk                                                |
| fcontrol.sys                     | 388950   | SODATSW spol。 s r.o.                                   |
| qfilter.sys                      | 388940   | 仲裁实验室                                            |
| Redlight.sys                     | 388930   | Trustware Ltd                                          |
| eps.sys                          | 388920   | Lumension                                              |
| VHDTrack.sys                     | 388915   | Intronis Inc                                           |
| VHDDelta.sys                     | 388912   | Niriva LLC                                             |
| FSTrace.sys                      | 388910   | Niriva LLC                                             |
| YahooStorage.sys                 | 388900   | Yahoo Japan Corporation                                |
| KeWF.sys                         | 388890   | KEBA AG                                                |
| epregflt.sys                     | 388888   | 检查点软件                                   |
| zsfprt.sys                       | 388880   | k4solution Co.                                         |
| dsflt.sys                        | 388876   | cEncrypt                                               |
| bfaccess.sys                     | 388872   | bitFence Inc.                                          |
| xcpl.sys                         | 388870   | X 云系统                                        |
| RMPHVMonitor.sys                 | 388865   | ManageEngine Zoho                                      |
| FAPMonitor.sys                   | 388864   | ManageEngine Zoho                                      |
| EaseFlt.sys                      | 388860   | EaseVault Technologies Inc.                            |
| sieflt.sys                       | 388852   | 快速修复技术 Pvt。 Ltd.                      |
| cssdlp.sys                       | 388851   | 快速修复技术 Pvt。 Ltd.                      |
| cssdlp.sys                       | 388850   | CoSoSys                                                |
| INISBDrv64.sys                   | 388840   | Initech Inc.                                           |
| trace.sys                        | 388831   | Fitsec Ltd                                             |
| SandDriver.sys                   | 388830   | Fitsec Ltd                                             |
| dskmn.sys                        | 388820   | Honeycomb 技术                                 |
| xkfsfd.sys                       | 388810   | Jiransoft Co., Ltd                                     |
| pcpifd.sys                       | 388800   | Jiransoft Co., Ltd                                     |
| NNTInfo.sys                      | 388790   | 新的 Net 技术限制                           |
| FsMonitor.sys                    | 388780   | IBM                                                    |
| CVCBT.sys                        | 388770   | CommVault Systems, Inc.                                |
| AwareCore.sys                    | 388760   | TaaSera                                                |
| laFS.sys                         | 388750   | NetworkProfi ltd.                                      |
| fsnk.sys                         | 388740   | SoftPerfect 研究                                   |
| RGNT.sys                         | 388730   | HFN                                                    |
| fltRs329.sys                     | 388720   | Secured Globe Inc.                                     |
| ospmon.sys                       | 388710   | SC ODEKIN 解决方案 SRL                                |
| edsigk.sys                       | 388700   | Enterprise Data Solutions, Inc.                        |
| fiometer.sys                     | 388692   | 合成 io                                              |
| dcSnapRestore.sys                | 388690   | 合成 io                                              |
| fam.sys                          | 388680   | 快速修复技术 Pvt。 Ltd.                      |
| vidderfs.sys                     | 388675   | Vidder Inc.                                            |    
| Tritiumfltr.sys                  | 388670   | Tritium Inc.                                           |
| HexisFSMonitor.sys               | 388660   | Hexis 网络解决方案                                  |
| BlackbirdFSA.sys                 | 388650   | BeyondTrust Inc.                                       |
| TMUMS.sys                        | 388642   | Trend Micro Inc.                                       |
| hfileflt.sys                     | 388640   | Trend Micro Inc.                                       |
| TMUMH.sys                        | 388630   | Trend Micro Inc.                                       |
| AcDriver.sys                     | 388620   | Trend Micro, Inc.                                      |
| SakFile.sys                      | 388610   | Trend Micro, Inc.                                      |
| SakMFile.sys                     | 388600   | Trend Micro, Inc.                                      |
| rsfdrv.sys                       | 388580   | Clonix Co                                              |
| alcapture.sys                    | 388570   | 太空飞船数字 Pty Ltd                                |
| kmNWCH.sys                       | 388560   | IGLOO SECURITY，inc                                   |
| ISIRMFmon.sys                    | 388550   | 安装 ALPS 系统集成 CO。                           |
| heimdall.sys                     | 388540   | Arkoon 网络安全                                |
| thetta.sys                       | 388532   | Syncopate                                              |
| thetta.sys                       | 388531   | Syncopate                                              |
| thetta.sys                       | 388530   | Syncopate                                              |
| DTPL.sys                         | 388520   | 连接 SHIFT LTD                                      |
| CyOptics.sys                     | 388514   | Cylance Inc.                                           |
| CyProtectDrv32.sys               | 388510   | Cylance Inc.                                           |
| CyProtectDrv64.sys               | 388510   | Cylance Inc.                                           |
| tbfsfilt.sys                     | 388500   | 第三个队列                                          |
| LDSecDrv.sys                     | 388490   | LANDESK 软件                                       |
| SGResFlt.sys                     | 388480   | Samsung SDS Ltd                                        |
| CwMem2k64.sys                    | 388470   | ApSoft                                                 |
| axfltdrv.sys                     | 388460   | Axact Pvt Ltd                                          |
| RMDiskMon.sys                    | 388450   | Qingdao Ruanmei 网络技术 Co.                 |
| diskactmon.sys                   | 388440   | Qingdao Ruanmei 网络技术 Co.                 |
| Codex.sys                        | 388430   | GameHi Co.                                             |
| CatMF.sys                        | 388420   | Logichron                                              |
| RW7FsFlt.sys                     | 388410   | PJSC KP VTI                                            |
| aswSP.sys                        | 388401   | Avast 软件                                         |
| aswFsBlk.sys                     | 388400   | ALWIL 软件                                         |
| ThreatStackFIM.sys               | 388380   | 威胁堆栈                                           |
| BOsCmFlt.sys                     | 388370   | Barkly Protects Inc.                                   |
| BOsFsFltr.sys                    | 388370   | Barkly Protects Inc.                                   |
| FeKern.sys                       | 388360   | FireEye Inc.                                           |
| libwamf.sys                      | 388350   | OPSWAT Inc.                                            |
| szardrv.sys                      | 388345   | SaferZone Co.                                          |
| szdfmdrv.sys                     | 388340   | SaferZone Co.                                          |
| szdfmdrv_usb.sys                 | 388331   | SaferZone Co.                                          |
| sprtdrv.sys                      | 388330   | SaferZone Co.                                          |
| SWFsFltr.sys                     | 388320   | Solarwinds LLC                                         |
| flashaccelfs.sys                 | 388310   | 网络设备                                      |
| changelog.sys                    | 388300   | 网络设备                                      |
| stcvsm.sys                       | 388250   | StorageCraft 技术                                      |
| aUpDrv.sys                       | 388240   | ITSTATION Inc                                          |
| fshs.sys                         | 388222   | F-Secure                                               |
| fshs.sys                         | 388221   | F-Secure                                               |
| fsatp.sys                        | 388220   | F-Secure                                               |
| SecdoDriver.sys                  | 388210   | Secdo                                                  |
| TGFSMF.sys                       | 388200   | Tetraglyph 技术                                |
| evscase.sys                      | 388100   | March Hare Software Ltd                                |
| VSScanner.sys                    | 388050   | VoodooSoft                                             |
| tsifilemon.sys                   | 388012   | 对讲机                                               |
| MarSpy.sys                       | 388010   | 对讲机                                               |
| BrnFileLock.sys                  | 388000   | 蓝色凸缘网络                                    |
| BrnSecLock.sys                   | 387990   | 蓝色凸缘网络                                    |
| LCmPrintMon.sys                  | 387978   | YATEM 有限公司                                         |
| LCgAdMon.sys                     | 387977   | YATEM 有限公司                                         |
| LCmAdMon.sys                     | 387976   | YATEM 有限公司                                         |
| LCgFileMon.sys                   | 387975   | YATEM 有限公司                                         |
| LCmFile.sys                      | 387974   | YATEM 有限公司                                         |
| LCgFile.sys                      | 387972   | YATEM 有限公司                                         |
| LCmFileMon.sys                   | 387970   | YATEM 有限公司                                         |
| IridiumSwitch.sys                | 387960   | Confio                                                 |
| scensemon.sys                    | 387950   | Scense                                                 |
| ruaff.sys                        | 387940   | RUNEXY                                                 |
| bbfilter.sys                     | 387930   | derivo GmbH                                            |
| Bfmon.sys                        | 387920   | 有限的百度 （中国香港特别行政区）                              |
| bdsysmon.sys                     | 387912   | 百度联机网络                                   |
| BdRdFolder.sys                   | 387910   | 百度 （北京）                                        |
| pscff.sys                        | 387900   | Weing Co.，Ltd.                                         |
| fcnotify.sys                     | 387880   | TCXA ltd.                                              |
| aaf.sys                          | 387860   | Actifio Inc                                            |
| gddcv.sys                        | 387840   | G Data Software AG                                     |
| wgfile.sys                       | 387820   | 橙色 WERKS Inc                                       |
| zesfsmf.sys                      | 387800   | Novell                                                 |
| uamflt.sys                       | 387700   | Sevtechnotrans                                         |
| ehdrv.sys                        | 387600   | 重置，spol。 s r.o.                                     |
| Snilog.sys                       | 387500   | Systemneeds, Inc                                       |
| tss.sys                          | 387400   | Tiversa Inc                                            |
| LmDriver.sys                     | 387390   | 在软 Kft。                                           |
| WDCFilter.sys                    | 387330   | Interset Inc.                                          |
| altcbt.sys                       | 387320   | Altaro ltd.                                            |
| bapfecpt.sys                     | 387310   | BitArmor Systems, Inc                                  |
| bamfltr.sys                      | 387300   | BitArmor Systems, Inc                                  |
| TrustedEdgeFfd.sys               | 387200   | FileTek, Inc.                                          |
| MRxGoogle.sys                    | 387100   | Google, Inc.                                           |
| YFSDR.SYS                        | 387010   | Yokogawa R&L Corp                                      |
| YFSD.SYS                         | 387000   | Yokogawa R&L Corp                                      |
| YFSRD.sys                        | 386990   | Yokogawa R&L Corp                                      |
| psgfoctrl.sys                    | 386990   | Yokogawa R&L Corp                                      |
| USBPDH.SYS                       | 386901   | 高级计算开发中心           |
| pecfilter.sys                    | 386900   | C DAC 海得拉巴                                        |
| GKPFCB.sys                       | 386810   | INCA Internet Co.                                      |
| GKPFCB64.sys                     | 386810   | INCA Internet Co.                                      |
| 在 32 位 TkPcFtCb.sys            | 386800   | INCA Internet Co.,Ltd.                                 |
| 64 位上的 TkPcFtCb64.sys          | 386800   | INCA Internet Co.,Ltd.                                 |
| bmregdrv.sys                     | 386731   | Yandex LLC                                             |
| bmfsdrv.sys                      | 386730   | Yandex LLC                                             |
| CarbonBlackK.sys                 | 386720   | Bit9 Inc.                                              |
| ScAuthFSFlt.sys                  | 386710   | LLC 的安全代码                                      |
| ScAuthIoDrv.sys                  | 386700   | LLC 的安全代码                                      |
| mfeaskm.sys                      | 386610   | McAfee                                                 |
| mfencfilter.sys                  | 386600   | McAfee                                                 |
| WinFLAHdrv.sys                   | 386540   | NewSoftwares.net                                       |
| WinFLAdrv.sys                    | 386530   | NewSoftwares.net                                       |
| WinDBdrv.sys                     | 386520   | NewSoftwares.net,Inc.                                  |
| WinFLdrv.sys                     | 386510   | NewSoftwares.net,Inc.                                  |
| WinFPdrv.sys                     | 386500   | NewSoftwares.net,Inc.                                  |
| SkyAMDrv.sys                     | 386430   | 天空 Co.                                                |
| SheedSelfProtection.sys          | 386421   | SheedSoft Ltd                                          |
| arta.sys                         | 386420   | SheedSoft Ltd.                                         |
| ApexSqlFilterDriver.sys          | 386410   | ApexSQL LLC                                            |
| stflt.sys                        | 386400   | Xacti                                                  |
| tbrdrv.sys                       | 386390   | 爬网程序组                                          |
| WinTeonMiniFilter.sys            | 386320   | Dmitry Stefankov                                       |
| wiper.sys                        | 386310   | Dmitry Stefankov                                       |
| DevMonMiniFilter.sys             | 386300   | Dmitry Stefankov                                       |
| VMWVvpfsd.sys                    | 386200   | VMware, Inc.                                           |
| RTOLogon.sys （重命名）           | 386200   | VMware, Inc.                                           |
| Code42Filter.sys                 | 386190   | Code42                                                 |
| FileGuard.sys                    | 386140   | RES 软件                                           |
| NetGuard.sys                     | 386130   | RES 软件                                           |
| RegGuard.sys                     | 386120   | RES 软件                                           |
| ImgGuard.sys                     | 386110   | RES 软件                                           |
| AppGuard.sys                     | 386100   | RES 软件                                           |
| minitrc.sys                      | 386020   | 受保护的网络                                     |
| cpepmon.sys                      | 386010   | Checkpoint Software                                    |
| CGWMF.sys                        | 386000   | NetIQ                                                  |
| ISRegFlt.sys                     | 385990   | Flexera Software                                       |
| ISRegFlt64.sys                   | 385990   | Flexera Software                                       |
| ctrPAMon.sys                     | 385960   | Comtrue 技术                                     |
| shdlpMedia.sys                   | 385950   | Comtrue 技术                                     |
| immflex.sys                      | 385910   | Immidio B.V.                                           |
| StegoProtect.sys                 | 385900   | Stegosystems                                           |
| brfilter.sys                     | 385890   | Bromium Inc                                            |
| BrCow_x_x_x_x.sys                | 385889   | Bromium Inc                                            |
| secRMM.sys                       | 385880   | Squadra Technologies                                   |
| dgfilter.sys                     | 385870   | DataGravity Inc.                                       |
| WFP_MRT.sys                      | 385860   | FireEye Inc                                            |
| mssecflt.sys                     | 385600   | Microsoft                                              |
| Backupreader.sys                 | 385500   | Microsoft                                              |
| AppVMon.sys                      | 385400   | Microsoft                                              |
| DpmFilter.sys                    | 385300   | Microsoft                                              |
| Sysmondrv.sys                    | 385201   | Microsoft                                              |
| Procmon11.sys                    | 385200   | Microsoft                                              |
| minispy.sys - Top                | 385100   | Microsoft                                              |
| fdrtrace.sys                     | 385001   | Microsoft                                              |
| filetrace.sys                    | 385000   | Microsoft                                              |
| uwfreg.sys                       | 384910   | Microsoft                                              |
| uwfs.sys                         | 384900   | Microsoft                                              |
| FilrDriver.sys                   | 383340   | Micro Focus                                            |
| rwchangedrv.sys                  | 383330   | Rackware                                               |
| airship-filter.sys               | 383320   | AIRWare 技术 Ltd                                 |
| AeFilter.sys                     | 383310   | Faronics Corporation                                   |
| QQProtect.sys                    | 383300   | 腾讯 （深圳）                                     |
| QQProtectX64.sys                 | 383300   | 腾讯 （深圳）                                     |
| KernelAgent32.sys                | 383260   | ZoneFox                                                |
| WRDWIZFILEPROT.SYS               | 383251   | WardWiz                                                |    
| WRDWIZREGPROT.SYS                | 383250   | WardWiz                                                |
| groundling32.sys                 | 383200   | Dell Secureworks                                       |
| groundling64.sys                 | 383200   | Dell Secureworks                                       |
| avgtpx86.sys                     | 383190   | AVG 技术 CZ                                    |
| avgtpx64.sys                     | 383190   | AVG 技术 CZ                                    |
| DataNow\_Driver.sys              | 383182   | AppSense Ltd                                           |
| UcaFltDriver.sys                 | 383180   | AppSense Ltd                                           |
| YFSD2.sys                        | 383170   | Yokogawa Corpration                                    |
| Kisknl.sys                       | 383160   | kingsoft                                               |
| MWatcher.sys                     | 383150   | Neowiz Corporation                                     |
| tsifilemon.sys                   | 383140   | 对讲机                                               |
| FIM.sys                          | 383130   | eIQnetworks                                            |
| cFSfdrv                          | 383120   | Chaewool                                               |
| ajfsprot.sys                     | 383110   | Analytik Jena AG                                       |
| isafermon                        | 383100   | (c)短信                                                 |
| kfac.sys                         | 383000   | 北京 CA JinChen 软件 Co.                        |
| GUMHFilter.sys                   | 382910   | Glarysoft Ltd.                                         |
| FJGSDis2.sys                     | 382900   | FUJITSU LIMITED                                        |
| secure_os.sys                    | 382890   | FUJITSU 社交科学                                 |
| zqFilter                         | 382800   | magrasoft Ltd                                          |
| ntps\_fa.sys                     | 382700   | NTP Software                                           |
| sConnect.sys                     | 382600   | I/O 数据设备                                        |
| AdaptivaClientCache32.sys        | 382500   | Adaptiva                                               |
| AdaptivaclientCache64.sys        | 382500   | Adaptiva                                               |
| GoFSMF.sys                       | 382430   | Gorizonty Rosta Ltd                                    |
| SWCommFltr.sys                   | 382420   | SnoopWall LLC                                          |
| atflt.sys                        | 382410   | Atlansys Software                                      |
| amfd.sys                         | 382400   | Atlansys Software                                      |
| iSafeKrnl.sys                    | 382390   | Elex 技术 Inc                                          |
| iSafeKrnlMon.sys                 | 382380   | Elex 技术 Inc                                          |
| 360box.sys                       | 382310   | Qihoo 360                                              |
| 360fsflt.sys                     | 382300   | 北京 Qihoo 技术 Co.                           |
| scred.sys                        | 382210   | SoftCamp Co.                                           |
| PDGenFam.sys                     | 382200   | Soluto LTD                                             |
| MCFileMon64.sys (x64 systems)    | 382100   | 三井 Electric ltd.                                 |
| MCFileMon32.sys (x 32 系统）    | 382100   | 三井 Electric ltd.                                 |
| RyGuard.sys                      | 382050   | 深圳 UNNOO 信息 Techco。                     |
| FileShareMon.sys                 | 382040   | 深圳 UNNOO 信息 Techco。                     |
| ryfilter.sys                     | 382030   | 深圳 UNNOO 信息 Techco。                     |
| secufile.sys                     | 382020   | 深圳 Unnoo LTD                                     |
| XiaobaiFs.sys                    | 382010   | 深圳 Unnoo LTD                                     |
| XiaobaiFsR.sys                   | 382000   | 深圳 Unnoo LTD                                     |
| TWBDCFilter.sys                  | 381910   | 开发                                              |
| VPDrvNt.sys                      | 381900   | AhnLab, Inc.                                           |
| eetd32.sys                       | 381800   | Entrust Inc.                                           |
| eetd64.sys                       | 381800   | Entrust Inc.                                           |
| dnaFSMonitor.sys                 | 381700   | Dtex 系统                                           |
| 在 2000 iwhlp2.sys               | 381610   | InfoWatch                                              |
| 在 XP 上 iwhlpxp.sys                | 381610   | InfoWatch                                              |
| 在 Vista 上 iwhlp.sys               | 381610   | InfoWatch                                              |
| iwdmfs.sys                       | 381600   | InfoWatch                                              |
| IronGateFD.sys                   | 381500   | rubysoft                                               |
| MagicBackupMonitor.sys           | 381400   | Magic Softworks, Inc.                                  |
| Sonar.sys                        | 381337   | IKARUS 安全                                        |
| IPFilter.sys                     | 381310   | Jinfengshuntai                                         |
| MSpy.sys                         | 381300   | Ladislav Zezula                                        |
| inuse.sys                        | 381200   | March Hare Software Ltd                                |
| qfmon.sys                        | 381190   | 质量 Corporation                                    |
| flyfs.sys                        | 381160   | NEC Soft                                               |
| serfs.sys                        | 381150   | NEC Soft                                               |
| hdrfs.sys                        | 381140   | NEC Soft                                               |
| UVMCIFSF.sys                     | 381130   | NEC Corporation                                        |
| ICFClientFlt.sys                 | 381120   | NEC 系统技术，ltd.                           |
| IccFileIoAd.sys                  | 381110   | NEC 系统技术，ltd.                           |
| IccFilterAudit.sys               | 381100   | NEC System 技术                                |
| IccFilterSc.sys                  | 381090   | InfoCage                                               |
| mtsvcdf.sys                      | 381000   | CristaLink                                             |
| SQLsafeFilterDriver.sys          | 380901   | Idera 软件                                         |
| IderaFilterDriver.sys            | 380900   | Idera                                                  |
| xhunter1.sys                     | 380800   | Wellbia.com                                            |
| iGuard.sys                       | 380720   | i-Guard SAS                                            |
| cbfltfs4.sys                     | 380710   | 备份系统 Ltd                                     |
| PkgFilter.sys                    | 380700   | 可缩放的软件                                      |
| snimg.sys                        | 380600   | Softnext 技术                                  |
| SK.sys                           | 380520   | 热软件                                          |
| mpxmon.sys                       | 380510   | 正技术                                  |
| KC3.sys                          | 380500   | Infotecs                                               |
| PLPOffDrv.sys                    | 380492   | SK Infosec Co                                          |
| ISFPDrv.sys                      | 380491   | SK Infosec Co                                          |
| ionmonwdrv.sys                   | 380490   | SK Infosec Co                                          |
| CbSampleDrv.sys                  | 380020   | Microsoft                                              |
| CbSampleDrv.sys                  | 380010   | Microsoft                                              |
| CbSampleDrv.sys                  | 380000   | Microsoft                                              |
| simrep.sys                       | 371100   | Microsoft                                              |
| change.sys                       | 370160   | Microsoft                                              |
| delete\_flt.sys                  | 370150   | Microsoft                                              |
| SmbResilFilter.sys               | 370140   | Microsoft                                              |
| usbtest.sys                      | 370130   | Microsoft                                              |
| NameChanger.sys                  | 370120   | Microsoft                                              |
| failMount.sys                    | 370110   | Microsoft                                              |
| failAttach.sys                   | 370100   | Microsoft                                              |
| stest.sys                        | 370090   | Microsoft                                              |
| cdo.sys                          | 370080   | Microsoft                                              |
| ctx.sys                          | 370070   | Microsoft                                              |
| fmm.sys                          | 370060   | Microsoft                                              |
| cancelSafe.sys                   | 370050   | Microsoft                                              |
| message.sys                      | 370040   | Microsoft                                              |
| passThrough.sys                  | 370030   | Microsoft                                              |
| nullFilter.sys                   | 370020   | Microsoft                                              |
| ntest.sys                        | 370010   | Microsoft                                              |
| minispy.sys - Middle             | 370000   | Microsoft                                              |
| nravwka.sys                      | 368400   | NURILAB                                                |
| bhkavki.sys                      | 368390   | NURILAB                                                |
| bhkavka.sys                      | 368390   | NURILAB                                                |
| docvmonk.sys                     | 368380   | NURILAB                                                |
| docvmonk64.sys                   | 368380   | NURILAB                                                |
| InvProtectDrv.sys                | 368370   | Invincea                                               |
| InvProtectDrv64.sys              | 368370   | Invincea                                               |
| browserMon.sys                   | 368360   | Adtrustmedia                                           |
| SfdFilter.sys                    | 368350   | Sandoll 通信                                  |
| phdcbtdrv.sys                    | 368340   | PHD Virtual Tech Inc.                                  |
| sysdiag.sys                      | 368330   | HeroBravo 技术                                   |
| cfrmd.sys                        | 368320   | Comodo 安全解决方案                              |
| repdrv.sys                       | 368310   | 视觉解决方案                                       |
| repdrv.sys                       | 368310   | 视觉解决方案                                       |
| repmon.sys                       | 368300   | 视觉解决方案                                       |
| cvofflineFlt32.sys               | 368200   | 量程 Corporation。                                   |
| cvofflineFlt64.sys               | 368200   | 量程 Corporation。                                   |
| DsDriver.sys                     | 368100   | Warp 磁盘软件                                     |
| nlcbhelpx86.sys                  | 368000   | NetLib                                                 |
| nlcbhelpx64.sys                  | 368000   | NetLib                                                 |
| nlcbhelpi64.sys                  | 368000   | NetLib                                                 |
| wbfilter.sys                     | 367950   | 白盒安全                                      |
| LRAgentMF.sys                    | 367900   | LogRhythm                                              |
| Drwebfwflt.sys                   | 367810   | 医生 Web                                             |
| EventMon.sys                     | 367800   | 医生 Web                                             |
| soidriver.sys                    | 367750   | Sophos Plc                                             |
| drvhookcsmf.sys                  | 367700   | GrammaTech, Inc.                                       |
| drvhookcsmf\_amd64.sys           | 367700   | GrammaTech, Inc.                                       |
| avipbb.sys                       | 367600   | Avira GmbH                                             |
| FileSightMF.sys                  | 367500   | PA 文件建立直通连接，                                          |
| csaam.sys                        | 367400   | Cisco 系统                                          |
| FSMon.sys                        | 367300   | 1mill                                                  |
| mfl.sys                          | 367200   | OSR Open Systems Resources, Inc.                       |
| filefilter.sys                   | 367100   | 北京 Zhong 挂起 Jiaxin 计算机网络科技有限公司 |
| iiscache.sys                     | 367000   | Microsoft                                              |
| nowonmf.sys                      | 366993   | 为 diskeeper Corporation                                  |
| dktlfsmf.sys                     | 366992   | 为 diskeeper Corporation                                  |
| DKDrv.sys                        | 366991   | 为 diskeeper Corporation                                  |
| DKRtWrt.sys-XPSP3 临时修复 | 366990   | 为 diskeeper Corporation                                  |
| HBFSFltr.sys                     | 366980   | 为 diskeeper Corporation                                  |
| xoiv8x64.sys                     | 366940   | Arcserve                                               |
| xomfcbt8x64.sys                  | 366930   | CA                                                     |
| KmxAgent.sys                     | 366920   | CA                                                     |
| KmxFile.sys                      | 366910   | CA                                                     |
| KmxSbx.sys                       | 366900   | CA                                                     |
| PointGuardVistaR32.sys           | 366810   | Futuresoft                                             |
| PointGuardVistaR64.sys           | 366810   | Futuresoft                                             |
| PointGuardVistaF.sys             | 366800   | Futuresoft                                             |
| PointGuardVista64F.sys           | 366800   | Futuresoft                                             |
| vintmfs.sys                      | 366789   | CondusivTechnologies                                   |
| hiofs.sys                        | 366782   | Condusiv 技术                                  |
| intmfs.sys                       | 366781   | CondusivTechnologies                                   |
| excfs.sys                        | 366780   | CondusivTechnologies                                   |
| zampit\_ml.sys                   | 366700   | Zampit                                                 |
| rflog.sys                        | 366600   | AppStream, Inc.                                        |
| LivedriveFilter.sys              | 366500   | Livedrive Internet Ltd                                 |
| regmonex.sys                     | 366410   | Tranxition Corp                                        |
| TXRegMon.sys                     | 366400   | Tranxition Corp                                        |
| SDVFilter.sys                    | 366300   | Soliton 系统 K.K.                                   |
| eLock2FSCTLDriver.sys            | 366210   | Egis 技术 inc.保留所有权利。                                   |
| msiodrv4.sys                     | 366200   | Centennial Software Ltd                                |
| mmPsy32.sys                      | 366110   | Resplendence 软件项目                         |
| mmPsy64.sys                      | 366110   | Resplendence 软件项目                         |
| rrMon32.sys                      | 366100   | Resplendence 软件项目                         |
| rrMon64.sys                      | 366100   | Resplendence 软件项目                         |
| cvsflt.sys                       | 366000   | March Hare Software Ltd                                |
| ktsyncfsflt.sys                  | 365920   | KnowledgeTree Inc.                                     |
| nvmon.sys                        | 365900   | NetVision, Inc.                                        |
| SnDacs.sys                       | 365810   | Informzaschita                                         |
| SnExequota.sys                   | 365800   | Informzaschita                                         |
| llfilter.sys                     | 365700   | SecureAxis Software                                    |
| hafsnk.sys                       | 365660   | HA Unix Pt                                             |
| DgeDriver.sys                    | 365655   | Dell Software Inc.                                     |
| BWFSDrv.sys                      | 365650   | Quest Software Inc.                                    |
| QFAPFlt.sys                      | 365600   | Quest Software                                         |
| XendowFLT.sys                    | 365570   | Credant 技术                                   |
| fmdrive.sys                      | 365500   | Cigital, Inc.                                          |
| EGMinFlt.sys                     | 365400   | WhiteCell Software Inc.                                |
| it2reg.sys                       | 365315   | Soliton 系统                                        |
| it2drv.sys                       | 365310   | Soliton 系统                                        |
| solitkm.sys                      | 365300   | Soliton 系统                                        |
| pgpwdefs.sys                     | 365270   | Symantec                                               |
| GEProtection.sys                 | 365260   | Symantec                                               |
| diflt.sys                        | 365260   | Symantec corp.                                         |
| sysMon.sys                       | 365250   | Symantec                                               |
| ssrfsf.sys                       | 365210   | Symantec                                               |
| emxdrv2.sys                      | 365200   | Symantec                                               |
| reghook.sys                      | 365150   | Symantec                                               |
| spbbcdrv.sys                     | 365100   | Symantec                                               |
| bhdrvx86.sys                     | 365100   | Symantec                                               |
| bhdrvx64.sys                     | 365100   | Symantec                                               |
| SISIPSFileFilter                 | 365010   | Symantec                                               |
| symevent.sys                     | 365000   | Symantec                                               |
| wrpfv.sys                        | 364900   | Microsoft                                              |
| UpGuardRealTime.sys              | 364810   | UpGuard                                                |
| usbl\_ifsfltr.sys                | 364800   | SecureAxis                                             |
| ntfsf.sys                        | 364700   | Sun 和木增加                                          |
| BssAudit.sys                     | 364600   | ByStorm                                                |
| GPMiniFIlter.sys                 | 364500   | Kalpataru                                              |
| AlfaFF.sys                       | 364400   | Alfa                                                   |
| FSAFilter.sys                    | 364300   | ScriptLogic                                            |
| GcfFilter.sys                    | 364200   | GemacmbH                                               |
| FFCFILT.SYS                      | 364100   | FFC Limited                                            |
| msnfsflt.sys                     | 364000   | Microsoft                                              |
| mblmon.sys                       | 363900   | Packeteer                                              |
| amsfilter.sys                    | 363800   | Axur 信息数秒。                                  |
| strapvista.sys （已停用）         | 363700   | AvSoft Technologies                                    |
| SAFE-Agent.sys                   | 363636   | SAFE-Cyberdefense                                      |
| EstPrmon.sys                     | 363610   | ESTsoft corp。                                          |
| Estprp.sys - 64bit               | 363610   | ESTsoft corp。                                          |
| EstRegmon.sys                    | 363600   | ESTsoft corp。                                          |
| EstRegp.sys - 64bit              | 363600   | ESTsoft corp。                                          |
| agfsmon.sys                      | 363530   | TechnoKom ltd.                                         |
| NlxFF.sys                        | 363520   | OnGuard 系统 LLC                                    |
| Sahara.sys                       | 363511   | Safend                                                 |
| Santa.sys                        | 363510   | Safend                                                 |
| vfdrv.sys                        | 363500   | Viewfinity                                             |
| xhunter64.sys                    | 363400   | Wellbia.com                                            |
| SPIMiniFilter.sys                | 363300   | 软件需要                                      |
| mracdrv.sys                      | 363230   | Mail.Ru                                                |
| BEDaisy.sys                      | 363220   | BattlEye 创新                                   |
| NetAccCtrl.sys                   | 363200   | 链接 co。                                               |
| NetAccCtrl64.sys                 | 363200   | 链接 co。                                               |
| hpreg.sys                        | 363130   | HP                                                     |
| qfimdvr.sys                      | 363120   | Qualys Inc.                                            |
| dsfemon.sys                      | 363100   | 拓扑 Ltd                                           |
| dsfemon.sys                      | 363100   | 拓扑 Ltd                                           |
| AmznMon.sys                      | 363030   | Amazon Web Services Inc                                |
| iothorfs.sys                     | 363020   | ioScience                                              |
| ctamflt.sys                      | 363010   | ComTrade                                               |
| psisolator.sys                   | 363000   | SharpCrafters                                          |
| QmInspec.sys                     | 362990   | 北京 QiAnXin 技术。                                  |
| GagSecurity.sys                  | 362970   | 北京 Shu Yan 科学                                |
| CybKernelTracker.sys             | 362960   | CyberArk 软件                                      |
| filemon.sys                      | 362950   | Temasoft 公司                                        |
| klifks.sys                       | 362902   | Kaspersky 实验室                                          |
| klifaa.sys                       | 362901   | Kaspersky 实验室                                          |
| Klifsm.sys                       | 362900   | Kaspersky 实验室                                          |
| minispy.sys - Bottom             | 361000   | Microsoft                                              |



## <a name="span-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespan340000---349999-fsfilter-undelete"></a><span id="340000_-_349999__FSFilter_Undelete"></span><span id="340000_-_349999__fsfilter_undelete"></span><span id="340000_-_349999__FSFILTER_UNDELETE"></span>340000 - 349999:FSFilter 撤消删除


| 微筛选器       | 海拔高度 | 公司                        |
|------------------|----------|--------------------------------|
| BSSFlt.sys       | 346000   | Blue Shoe Software LLC         |
| ThinIO.sys       | 345900   | ThinScale 技术           |
| hmpalert.sys     | 345800   | SurfRight                      |
| nsffkmd64.sys    | 345700   | NetSTAR Inc.                   |
| nsffkmd32.sys    | 345700   | NetSTAR Inc.                   |
| xbprocfilter.sys | 345600   | Zrxb                           |
| ifileguard.sys   | 345500   | I-O DATA DEVICE, INC.          |
| undelex32.sys    | 345400   | Resplendence 软件项目 |
| undelex64.sys    | 345400   | Resplendence 软件项目 |
| starmon.sys      | 345300   | Kantowitz Engineering, Inc.    |
| mxRCycle.sys     | 345200   | Avanquest                      |
| UdFilter.sys     | 345100   | 为 diskeeper Corporation          |
| it2prtc.sys      | 345040   | Soliton 系统 K.K.           |
| SolRegFilter.sys | 345030   | Soliton 系统 K.K.           |
| SolSecBr.sys     | 345020   | Soliton 系统 K.K.           |
| SolFCLLi.sys     | 345010   | Soliton 系统 K.K.           |
| SolFCL.sys       | 345000   | Soliton 智能秒              |



## <a name="span-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspan320000---329998-fsfilter-anti-virus"></a><span id="320000_-_329998__FSFilter_Anti-Virus"></span><span id="320000_-_329998__fsfilter_anti-virus"></span><span id="320000_-_329998__FSFILTER_ANTI-VIRUS"></span>320000 - 329998:FSFilter 防病毒软件


| 微筛选器                       | 海拔高度 | 公司                                                   |
|----------------------------------|----------|-----------------------------------------------------------|
| DeepInsFS.sys                    | 329190   | 深度想到                                             |
| AppCheckD.sys                    | 329180   | CheckMAL Inc                                              |
| spellmon.sys                     | 329170   | SpellSecurity                                             |
| WhiteShield.sys                  | 329160   | Meidensha Corp                                            |
| reaqtor.sys                      | 329150   | ReaQta ltd.                                               |
| SE46Filter.sys                   | 329140   | 技术 Nexus AB                                       |
| FileScan.sys                     | 329130   | NPcore Ltd                                                |
| ECATDriver.sys                   | 329120   | EMC                                                       |
| pfkrnl.sys                       | 329110   | FXSEC LTD                                                 |
| epicFilter.sys                   | 329100   | 隐藏的单反                                             |
| b9kernel.sys                     | 329050   | Bit9 Inc                                                  |
| eeCtrl.sys                       | 329010   | Symantec                                                  |
| eraser.sys （已停用）             | 329010   | Symantec                                                  |
| SRTSP.sys,                       | 329000   | Symantec                                                  |
| SRTSPIT.sys-ia64 系统       | 329000   | Symantec                                                  |
| SRTSP64.SYS - x64 systems        | 329000   | Symantec                                                  |
| a2ertpx86.sys                    | 328920   | Emsi Software GmbH                                        |
| a2ertpx64.sys                    | 328920   | Emsi Software GmbH                                        |
| a2gffx86.sys - x86               | 328910   | Emsi Software GmbH                                        |
| a2gffx64.sys - x64               | 328910   | Emsi Software GmbH                                        |
| a2gffi64.sys - IA64              | 328910   | Emsi Software GmbH                                        |
| a2acc.sys                        | 328900   | Emsi Software GmbH                                        |
| 在 x64 上的 a2acc64.sys 系统       | 328900   | Emsi Software GmbH                                        |
| si32\_file.sys                   | 328810   | Scargo Inc                                                |
| si64\_file.sys                   | 328810   | Scargo Inc                                                |
| mbam.sys                         | 328800   | Malwarebytes corp.                                        |
| KUBWKSP.sys                      | 328750   | Netlor SAS                                                |
| hcp_kernel_acq.sys               | 328740   | refractionPOINT                                           |
| SegiraAM.sys                     | 328730   | Segira LLC                                                |
| wdocsafe.sys                     | 328722   | Cheetah Mobile Inc.                                       |
| lbprotect.sys                    | 328720   | Cheetah Mobile Inc.                                       |
| eamonm.sys                       | 328700   | 重置，spol。 s r.o.                                        |
| MaxProc64.sys                    | 328620   | 最大安全软件                                       |
| MaxProtector.sys                 | 328610   | 最大安全软件                                       |
| SDActMon.sys                     | 328600   | 最大安全软件                                       |
| fileflt.sys                      | 328540   | Trend Micro Inc.                                          |
| TmEsFlt.sys                      | 328530   | Trend Micro Inc.                                          |
| tmevtmgr.sys                     | 328510   | Trend Micro Inc.                                          |
| tmpreflt.sys                     | 328500   | 趋势                                                     |
| vcMFilter.sys                    | 328400   | SGRI Co.，LTD.                                            |
| SAFsFilter.sys                   | 328300   | Lightspeed 系统                                        |
| vsepflt.sys                      | 328200   | VMware                                                    |
| VFileFilter.sys(renamed)         | 328200   | VMware                                                    |
| drivesentryfilterdriver2lite.sys | 328100   | DriveSentry Inc                                           |
| WdFilter.sys                     | 328010   | Microsoft                                                 |
| mpFilter.sys                     | 328000   | Microsoft                                                 |
| vrSDetri.sys                     | 327801   | ETRI                                                      |
| vrSDetrix.sys                    | 327800   | ETRI                                                      |
| AhkSvPro.sys                     | 327720   | Ahkun Co.                                                 |
| AhkUsbFW.sys                     | 327710   | Ahkun Co.                                                 |
| AhkAMFlt.sys                     | 327700   | Ahkun Co.                                                 |
| PSINPROC.SYS                     | 327620   | Panda 安全                                            |
| PSINFILE.SYS                     | 327610   | Panda 安全                                            |
| amfsm.sys - Windows XP/2003 x64  | 327600   | Panda 安全                                            |
| amm8660.sys - Windows Vista x86  | 327600   | Panda 安全                                            |
| amm6460.sys - Windows Vista x64  | 327600   | Panda 安全                                            |
| ADSpiderDoc.sys                  | 327550   | Digitalonnet                                              |
| BkavSdFlt.sys                    | 327540   | Bkav Corporation                                          |
| easyanticheat.sys                | 327530   | EasyAntiCheat 解决方案                                   |
| 5nine.cbt.sys                    | 327520   | 5nine Software                                            |
| caavFltr.sys                     | 327510   | 计算机 Assoc                                            |
| ino\_fltr.sys                    | 327500   | 计算机 Assoc                                            |
| WCSDriver.sys                    | 327410   | 白色云安全                                      |
| 360qpesv.sys                     | 327404   | 360 软件 （北京）                                    |
| dsark.sys                        | 327402   | Qihoo 360                                                 |
| 360avflt.sys                     | 327400   | Qihoo 360                                                 |
| ANVfsm.sys                       | 327310   | Arcdo                                                     |
| CDrRSFlt.sys                     | 327300   | Arcdo                                                     |
| EPSMn.sys                        | 327200   | SGA                                                       |
| VTSysFlt.sys                     | 327150   | 北京 Venus                                             |
| TesMon.sys                       | 327130   | 腾讯                                                   |
| QQSysMonX64.sys                  | 327125   | 腾讯                                                   |
| QQSysMon.sys                     | 327120   | 腾讯                                                   |
| TSysCare.sys                     | 327110   | 深圳腾讯计算机系统公司限制         |
| TFsFlt.sys                       | 327100   | 深圳腾讯计算机系统公司限制         |
| avmf.sys                         | 327000   | Authentium                                                |
| BDFileDefend.sys                 | 326916   | 百度 （北京）                                           |
| BDsdKit.sys                      | 326914   | 百度联机网络技术 （北京） Co.              |
| bd0003.sys                       | 326912   | 百度联机网络技术 （北京） Co.              |
| Bfilter.sys                      | 326910   | 有限的百度 （中国香港特别行政区）                                 |
| NeoKerbyFilter                   | 326900   | NeoAutus                                                  |
| PLGFltr.sys                      | 326800   | Paretologic                                               |
| WrdWizSecure64.sys               | 326730   | WardWiz                                                   |
| wrdwizscanner.sys                | 326720   | WardWiz                                                   |
| AshAvScan.sys                    | 326700   | Ashampoo GmbH & Co.KG                                    |
| Zyfm.sys                         | 326666   | ZhengYong InfoTech ltd.                                   |
| csaav.sys                        | 326600   | Cisco 系统                                             |
| oavfm.sys                        | 326550   | HSM IT 服务 Gmbh                                      |
| SegMD.sys                        | 326520   | Segurmatica                                               |
| SegMP.sys                        | 326510   | Segurmatica                                               |
| SegF.sys                         | 326500   | Segurmatica                                               |
| eeyehv.sys                       | 326400   | eEye 数字安全                                     |
| eeyehv64.sys                     | 326400   | eEye 数字安全                                     |
| CpAvFilter.sys                   | 326311   | CodeProof Technologies Inc                                |
| CpAvKernel.sys                   | 326310   | CodeProof Technologies Inc                                |
| NovaShield.sys                   | 326300   | Securitas Technologies,Inc.                               |
| SheedAntivirusFilterDriver.sys   | 326290   | SheedSoft Ltd                                             |
| bSyirmf.sys                      | 326260   | BLACKFORT 安全                                        |
| bSymfdm.sys                      | 326240   | BLACKFORT 安全                                        |
| bSyrtp.sys                       | 326230   | BLACKFORT 安全                                        |
| bSyaed.sys                       | 326220   | BLACKFORT 安全                                        |
| bSyar.sys                        | 326210   | BLACKFORT 安全                                        |
| BdFileSpy.sys                    | 326200   | BullGuard                                                 |
| npxgd.sys                        | 326160   | INCA Internet Co.                                         |
| npxgd64.sys                      | 326160   | INCA Internet Co.                                         |
| tkpl2k.sys                       | 326150   | INCA Internet Co.                                         |
| tkpl2k64.sys                     | 326150   | INCA Internet Co.                                         |
| GKFF.sys                         | 326140   | INCA Internet Co.                                         |
| GKFF64.sys                       | 326140   | INCA Internet Co.                                         |
| tkdac2k.sys                      | 326130   | INCA Internet Co.                                         |
| tkdacxp.sys                      | 326130   | INCA Internet Co.                                         |
| tkdacxp64.sys                    | 326130   | INCA Internet Co.                                         |
| tksp2k.sys                       | 326120   | INCA Internet Co.                                         |
| tkspxp.sys                       | 326120   | INCA Internet Co.                                         |
| tkspxp64.sys                     | 326120   | INCA Internet Co.                                         |
| tkfsft.sys                       | 326110   | INCA Internet Co., Ltd                                    |
| tkfsft64.sys - 64bit             | 326110   | INCA Internet Co., Ltd                                    |
| tkfsavxp.sys - 32bit             | 326100   | INCA Internet Co., Ltd                                    |
| tkfsavxp64.sys - 64bit           | 326100   | INCA Internet Co., Ltd                                    |
| SMDrvNt.sys                      | 326040   | AhnLab, Inc.                                              |
| ATamptNt.sys                     | 326030   | AhnLab, Inc.                                              |
| V3Flt2k.sys                      | 326020   | AhnLab, Inc.                                              |
| V3MifiNt.sys                     | 326010   | Ahnlab                                                    |
| V3Ift2k.sys                      | 326000   | Ahnlab                                                    |
| V3IftmNt.sys （旧名称）          | 326000   | Ahnlab                                                    |
| ArfMonNt.sys                     | 325990   | Ahnlab                                                    |
| AhnRghLh.sys                     | 325980   | Ahnlab                                                    |
| AszFltNt.sys                     | 325970   | Ahnlab                                                    |
| OMFltLh.sys                      | 325960   | Ahnlab                                                    |
| V3Flu2k.sys                      | 325950   | Ahnlab                                                    |
| TfFregNt.sys                     | 325940   | AhnLab Inc.                                               |
| vcdriv.sys                       | 325820   | Greatsoft Corp.Ltd                                        |
| vcreg.sys                        | 325810   | Greatsoft Corp.Ltd                                        |
| vchle.sys                        | 325800   | Greatsoft Corp.Ltd                                        |
| NxFsMon.sys                      | 325700   | Novatix Corporation                                       |
| AntiLeakFilter.sys               | 325600   | 单个开发人员 (Soft3304)                           |
| NanoAVMF.sys                     | 325510   | Panda 软件                                            |
| shldflt.sys                      | 325500   | Panda 软件                                            |
| nprosec.sys                      | 325410   | Norman ASA                                                |
| nregsec.sys                      | 325400   | Norman ASA                                                |
| issregistry.sys                  | 325300   | IBM                                                       |
| THFilter.sys                     | 325200   | Sybonic 系统 Inc                                       |
| pervac.sys                       | 325100   | PerSystems SA                                             |
| avgmfx86.sys                     | 325000   | AVG Grisoft                                               |
| avgmfx64.sys                     | 325000   | AVG Grisoft                                               |
| avgmfi64.sys                     | 325000   | AVG Grisoft                                               |
| avgmfrs.sys （已停用）            | 325000   | AVG Grisoft                                               |
| FortiAptFilter.sys               | 324930   | Fortinet Inc.                                             |
| fortimon2.sys                    | 324920   | Fortinet Inc.                                             |
| fortirmon.sys                    | 324910   | Fortinet Inc.                                             |
| fortishield.sys                  | 324900   | Fortinet Inc.                                             |
| mscan-rt.sys                     | 324800   | SecureBrain Corporation                                   |
| sysdiag.sys                      | 324600   | Huorong 安全                                          |
| agentrtm64.sys                   | 324510   | WINS CO。 LTD                                              |
| rswmon.sys                       | 324500   | WINS CO。 LTD                                              |
| mwfsmfltr.sys                    | 324420   | MicroWorld Software Services Pvt. Ltd.                    |
| gtkdrv.sys                       | 324410   | GridinSoft LLC                                            |
| GbpKm.sys                        | 324400   | 天然气 Tecnologia                                            |
| crnsysm.sys                      | 324310   | Coranti                                                   |
| crncache32.sys                   | 324300   | Coranti                                                   |
| crncache64.sys                   | 324300   | Coranti                                                   |
| drwebfwft.sys                    | 324210   | 医生 Web                                                |
| DwShield.sys                     | 324200   | 医生 Web                                                |
| DwShield64.sys                   | 324200   | 医生 Web                                                |
| IProtect.sys                     | 324150   | EveryZone                                                 |
| TvFiltr.sys                      | 324140   | EveryZone inc.保留所有权利。                                            |
| TvDriver.sys                     | 324130   | EveryZone inc.保留所有权利。                                            |
| TvSPFltr.sys                     | 324120   | EveryZone inc.保留所有权利。                                            |
| TvPtFile.sys                     | 324110   | EveryZone inc.保留所有权利。                                            |
| TvMFltr.sys                      | 324100   | Everyzone                                                 |
| SAVOnAccess.sys                  | 324010   | Sophos                                                    |
| savonaccess.sys                  | 324000   | Sophos                                                    |
| sld.sys                          | 323990   | Sophos                                                    |
| OADevice.sys                     | 323900   | 高 Emu                                                  |
| pwipf6.sys                       | 323800   | PWI, Inc.                                                 |
| EstRkmon.sys                     | 323700   | ESTsoft corp。                                             |
| EstRkr.sys - 64bit               | 323700   | ESTsoft corp。                                             |
| dwprot.sys                       | 323610   | 医生 Web                                                |
| Spiderg3.sys                     | 323600   | 医生 Web ltd.                                           |
| STKrnl64.sys                     | 323500   | Verdasys Inc                                              |
| UFDFilter.sys                    | 323400   | Yoggie                                                    |
| SCFltr.sys                       | 323300   | SecurtiyCoverage, Inc.                                    |
| fildds.sys                       | 323200   | Filseclab                                                 |
| fsfilter.sys                     | 323100   | MastedCode Ltd                                            |
| fpav\_rtp.sys                    | 323000   | f 保护                                                 |
| cwdriver.sys                     | 322900   | Leith 条形码                                                |
| AYFilter.sys                     | 322810   | ESTsoft                                                   |
| Rtw.sys                          | 322800   | ESTsoft                                                   |
| HookSys.sys                      | 322700   | 北京上升信息技术公司限制 |
| snscore.sys                      | 322600   | S.N.Safe&Software                                         |
| ssvhook.sys                      | 322500   | SecuLution GmbH                                           |
| strapvista.sys                   | 322400   | AvSoft Technologies                                       |
| strapvista64.sys                 | 322400   | AvSoft Technologies                                       |
| sascan.sys                       | 322300   | SecureAge 技术                                      |
| savant.sys                       | 322200   | Savant Protection, Inc.                                   |
| VrBBDFlt.sys                     | 322160   | HAURI                                                     |
| vrSDfmx.sys                      | 322153   | HAURI                                                     |
| vrSDfmx.sys                      | 322152   | HAURI                                                     |
| vrSDam.sys                       | 322151   | HAURI                                                     |
| vrSDam.sys                       | 322150   | HAURI                                                     |
| VRAPTFLT.sys                     | 322140   | HAURI inc.保留所有权利。                                                |
| VrAptDef.sys                     | 322130   | HAURI                                                     |
| VrSdCore.sys                     | 322120   | HAURI                                                     |
| VrFsFtM.sys                      | 322110   | HAURI                                                     |
| VrFsFtMX.sys(AMD64)              | 322110   | HAURI                                                     |
| vradfil2.sys                     | 322100   | HAURI                                                     |
| fsgk.sys                         | 322000   | f 安全                                                  |
| bouncer.sys                      | 321950   | CoreTrace Corporation                                     |
| PCTCore64.sys                    | 321910   | PC 工具 Pty. Ltd.                                        |
| PCTCore.sys （旧名称）           | 321910   | PC 工具 Pty. Ltd.                                        |
| ikfilesec.sys                    | 321900   | PC 工具 Pty. Ltd.                                        |
| ZxFsFilt.sys                     | 321800   | 澳大利亚项目                                       |
| antispyfilter.sys                | 321700   | C-NetMedia Inc                                            |
| PZDrvXP.sys                      | 321600   | VisionPower Co.，Ltd.                                      |
| ggc.sys                          | 321510   | 快速修复 TechnologiesPvt。 Ltd.                          |
| catflt.sys                       | 321500   | 快速修复 TechnologiesPvt。 Ltd.                          |
| bdsflt.sys                       | 321490   | 快速修复技术 Pvt。 Ltd.                         |
| arwflt.sys                       | 321480   | 快速修复技术 Pvt。 Ltd.                         |
| csagent.sys                      | 321410   | CrowdStrike ltd.                                          |
| kmkuflt.sys                      | 321400   | Komoku Inc.                                               |
| epdrv.sys                        | 321320   | McAfee Inc.                                               |
| mfencoas.sys                     | 321310   | McAfee Inc.                                               |
| mfehidk.sys                      | 321300   | McAfee Inc.                                               |
| swin.sys                         | 321250   | McAfee Inc.                                               |
| cmdccav.sys                      | 321210   |Comodo Group Inc.                                          |
| cmdguard.sys                     | 321200   | Comodo Group Inc.                                         |
| K7Sentry.sys                     | 321100   | K7 计算私有 ltd.                                 |
| nsminflt.sys                     | 321050   | NHN                                                       |
| nsminflt64.sys                   | 321050   | NHN                                                       |
| nvcmflt.sys                      | 321000   | Norman                                                    |
| dgsafe.sys                       | 320950   | 软件                                                  |
| issfltr.sys                      | 320900   | ISS                                                       |
| hbflt.sys                        | 320840   | BitDefender SRL                                           |
| bdsvm.sys                        | 320830   | Bitdefender                                               |
| gzflt.sys                        | 320820   | BitDefender SRL                                           |
| bddevflt.sys                     | 320812   | BitDefender SRL                                           |
| AVCKF.SYS                        | 320810   | BitDefender SRL                                           |
| bdfsfltr.sys                     | 320800   | Softwin                                                   |
| bdfm.sys                         | 320790   | Softwin                                                   |
| Atc.sys                          | 320781   | BitDefender SRL                                           |
| AVC3.SYS                         | 320780   | BitDefender SRL                                           |
| TRUFOS.SYS                       | 320770   | BitDefender SRL                                           |
| aswmonflt.sys                    | 320700   | Alwil                                                     |
| HookCentre.sys                   | 320602   | G 数据                                                    |
| PktIcpt.sys                      | 320601   | G 数据                                                    |
| MiniIcpt.sys                     | 320600   | G 数据                                                    |
| avgntflt.sys                     | 320500   | Avira GmbH                                                |
| klbg.sys                         | 320440   | Kaspersky                                                 |
| kldback.sys                      | 320430   | Kaspersky                                                 |
| kldlinf.sys                      | 320420   | Kaspersky                                                 |
| kldtool.sys                      | 320410   | Kaspersky                                                 |
| klif.sys                         | 320401   | Kaspersky 实验室                                             |
| klif.sys                         | 320400   | Kaspersky                                                 |
| avfsmn.sys                       | 320310   | Anvisoft                                                  |
| hssfwhl.sys                      | 320330   | 人： Hitachi Solutions                                         |
| DeepInsFS.sys                    | 320320   | 深度想到 ltd.                                        |
| avfsmn.sys                       | 320310   | Anvisoft                                                  |
| lbd.sys                          | 320300   | Lavasoft AB                                               |
| rvsmon.sys                       | 320200   | CJSC Returnil 软件                                    |
| ssfmonm.sys                      | 320100   | Webroot Software, Inc.                                    |
| VirtualAgent.sys                 | 320005   | Symantec                                                  |



## <a name="span-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspan300000---309998-fsfilter-replication"></a><span id="300000_-_309998__FSFilter_Replication"></span><span id="300000_-_309998__fsfilter_replication"></span><span id="300000_-_309998__FSFILTER_REPLICATION"></span>300000 - 309998:FSFilter 复制


| 微筛选器              | 海拔高度 | 公司                 |
|-------------------------|----------|-------------------------|
| IntelCAS.sys            | 309100   | Intel Corporation       |
| mvfs.sys                | 309000   | IBM Corporation         |
| fsrecord.sys            | 305000   | Microsoft               |
| InstMon.sys             | 304201   | Numecent inc.保留所有权利。           |    
| StreamingFSD.sys        | 304200   | Numecent inc.保留所有权利。           |
| ubcminifilterdriver.sys | 304100   | Ullmore ltd.            |
| replistor.sys           | 304000   | Legato                  |
| stfsd.sys               | 303900   | 工作技术  |
| xomf.sys                | 303800   | CA (XOSOFT)             |
| nfid.sys                | 303700   | 从不组 Ltd     |
| sybfilter.sys           | 303600   | Sybase, Inc.            |
| rfsfilter.sys           | 303500   | Evidian                 |
| cvmfsj.sys              | 303400   | CommVault Systems, Inc. |
| iOraFilter.sys          | 303300   | Infonic plc             |
| bkbmfd32.sys (x86)      | 303200   | BakBone Software, Inc   |
| bkbmfd64.sys (x64)      | 303200   | BakBone Software, Inc   |
| mblvn.sys               | 303100   | Packeteer               |
| AV12NFNT.sys            | 303000   | AhnLab                  |
| mDP\_win\_mini.sys      | 302900   | 宏的影响            |
| ctxubs.sys              | 302800   | Citrix Systems          |
| AxFilter.sys            | 301800   | Axcient                 |
| vxfsrep.sys             | 301700   | Symantec                |
| dellcapfd.sys           | 301600   | Dell                    |
| Sptres.sys              | 301500   | Safend                  |
| OfficeBackup.sys        | 301400   | Ushus 技术      |
| pcvnfilt.sys            | 301300   | Blue Coat               |
| repdac.sys              | 301200   | NSI                     |
| repkap.sys              | 301100   | NSI                     |
| repdrv.sys              | 301000   | NSI                     |



## <a name="span-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspan280000---289998-fsfilter-continuous-backup"></a><span id="280000_-_289998__FSFilter_Continuous_Backup"></span><span id="280000_-_289998__fsfilter_continuous_backup"></span><span id="280000_-_289998__FSFILTER_CONTINUOUS_BACKUP"></span>280000 - 289998:FSFilter 持续备份


| 微筛选器             | 海拔高度 | 公司               |
|------------------------|----------|-----------------------|
| Klcdp.sys              | 288900   | Kaspersky 实验室         |
| splitinfmon.sys        | 288800   | 拆分无穷大        |
| versamatic.sys         | 288700   | Acertant 技术         |
| Yfilemon.sys           | 288690   | Yarisoft              |
| ibac.sys               | 288600   | Idealstor，LLC。       |
| fkdriver.sys           | 288500   | Filekeeper            |
| AAFileFilter.sys       | 288300   | Dell                  |
| hyperoo.sys            | 288400   | Hyperoo Ltd           |
| HyperBacCA.sys         | 285000   | Red Gate 软件 Ltd |
| ZMSFsFltr.sys          | 284400   | 全盛 InfoTech       |
| aFsvDrv.sys            | 283100   | ITSTATION Inc         | 
| AlfaSC.sys             | 284300   | Alfa Corporation      |
| hie\_ifs.sys           | 284200   | Hie Electronics, Inc. |
| AAFs.sys               | 284100   | AppAssure 软件    |
| defilter.sys （旧版）     | 284000   | Microsoft             |
| tilana.sys             | 283000   | Tilana Sys            |
| VmDPFilter.sys         | 282900   | 宏的影响          |
| LbFilter.sys           | 281700   | Linkverse 公司      |
| fbsfd.sys              | 281600   | Ferro Software        |
| dupleemf.sys           | 281500   | Duplee SPI, S.L.      |
| file\_tracker.sys      | 281420   | Acronis               |
| exbackup.sys           | 281410   | Acronis               |
| afcdp.sys              | 281400   | Acronis, Inc.         |
| dcefltr.sys            | 281300   | Cofio Software Ltd    |
| ipmrsync\_mfilter.sys  | 281200   | OpenMars 企业  |
| cascade.sys            | 281100   | JP Software           |
| filearchive.sys        | 281000   | 代码总结           |
| syscdp.sys             | 280900   | 系统确定 AB          |
| dpnedriver.sys (x86)   | 280850   | HP                    |
| dpnedriver64.sys (x64) | 280850   | HP                    |
| hpchgflt.sys           | 280800   | HP                    |
| VirtFile.sys           | 280700   | Symantec              |
| DeqoCPS.sys            | 280600   | Deqo                  |
| LV\_Tracker.sys        | 280500   | LiveVault             |
| cpbak.sys              | 280410   | Checkpoint Software   |
| tdmonxp.sys            | 280400   | TimeData              |
| nvfr\_cpd              | 280310   | Bakbone 软件      |
| nvfr\_fdd              | 280300   | Bakbone 软件      |
| Sptbkp.sys             | 280290   | Safend                |



## <a name="span-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspan260000---269998-fsfilter-content-screener"></a><span id="260000_-_269998__FSFilter_Content_Screener"></span><span id="260000_-_269998__fsfilter_content_screener"></span><span id="260000_-_269998__FSFILTER_CONTENT_SCREENER"></span>260000 - 269998:FSFilter 内容筛选程序


|         微筛选器          | 海拔高度 |                 公司                  |
|-----------------------------|----------|------------------------------------------|
|        Klshadow.sys         |  268300  |              Kaspersky 实验室               |
|         isarsd.sys          |  268260  |                  ISARS                   |
|       zeoscanner.sys        |  268255  |                 PCKeeper                 |
|       fileHiders.sys        |  268250  |                 PCKeeper                 |
|   cbfltfs4-ObserveIT.sys    |  268240  |                ObserveIT                 |
|         hipara.sys          |  268230  |                Allsum LLC                |
|  AliFileMonitorDriver.sys   |  268220  |                 Alibaba                  |
|       writeGuard.sys        |  268210  |                TCXA ltd.                 |
|     KKUDKProtectKer.sys     |  268200  |        Goldmessage 技术共同。        |
|        Atomizer.sys         |  268160  |            DragonFlyCodeWorks            |
|         farwflt.sys         |  268150  |               Malwarebytes               |
|       ADSpiderEx2.sys       |  268140  |               Digitalonnet               |
|          Safe.sys           |  268120  |            rian@alum.mit.edu             |
|   mydlpdelete-scanner.sys   |  268110  |             Medra Teknoloji              |
|      mydlpscanner.sys       |  268100  |             Medra Teknoloji              |
|     DLDriverNetMini.sys     |  268030  |              DeviceLock Inc              |
|        ENFFLTDRV.sys        |  268020  |            Enforcive 系统             |
|         crocopg.sys         |  268010  |               Infomaximum                |
|         sbapifs.sys         |  268000  |             Sunbelt 软件             |
|         SGKD32.SYS          |  267910  |           NetSection 安全            |
|        IccFilter.sys        |  267900  |         NEC System 技术          |
|          tflbc.sys          |  267800  |       Tani 电子公司       |
|          WBDrv.sys          |  266700  |                Axiana LLC                |
|       DMSamFilter.sys       |  266600  |              Digimarc corp.              |
|        5nine.cbt.sys        |  266100  |              5nine Software              |
|          bsfs.sys           |  266000  |     快速修复 TechnologiesPvt。 Ltd.     |
|      XXRegSFilter.sys       |  265910  |     Zhe Jiang Xinxin 软件技术。      |
|        XXSFilter.sys        |  265900  |     Zhe Jiang Xinxin 软件技术。      |
|    AloahaUSBBlocker.sys     |  265800  |           Wrocklage Intermedia           |
|         frxdrv.sys          |  265700  |                 FSLogix                  |
|      FolderSecure.sys       |  265600  |           最大安全软件            |
|       XendowFLTC.sys        |  265570  |           Credant 技术           |
|           RepDac            |  265500  |             视觉解决方案             |
|        tbbdriver.sys        |  265400  |                  Tedesi                  |
|         spcgrd.sys          |  265300  |          FUJITSU 广泛解决方案          |
|         fdtlock.sys         |  265250  | FUJITSU 广泛解决方案和咨询 inc.保留所有权利。 |
|         ssfFSC.sys          |  265200  |              SECUWARE S.L。               |
|       GagSecurity.sys       |  265120  |         北京 Shu Yan 科学          |
|       PrintDriver.sys       |  265110  |         北京 Shu Yan 科学          |
|          activ.sys          |  265100  |            Rapidware Pty Ltd             |
|         avscan.sys          |  265010  |                Microsoft                 |
|         scanner.sys         |  265000  |                Microsoft                 |
|         DI\_fs.sys          |  264910  |                 Soft-SB                  |
|         wgnpos.sys          |  264900  |                Orchestria                |
|         odfltr.sys          |  264810  |          NetClean 技术           |
|        ncpafltr.sys         |  264800  |          NetClean 技术           |
|           ct.sys            |  264700  |               Haute 安全               |
|         fvefsmf.sys         |  264600  |            Fortisphere, Inc.             |
|          block.sys          |  264500  |         自治系统限制         |
|         csascr.sys          |  264400  |              Cisco 系统               |
|         SymAFR.sys          |  264300  |           Symantec Corporation           |
|          cwnep.sys          |  264200  |              Websense Inc.               |
|     spywareremover.sys      |  264150  |                C-Netmedia                |
|       malwarebot.sys        |  264140  |                C-Netmedia                |
|     antispywarebot.sys      |  264130  |              2Squared Inc.               |
|        adwarebot.sys        |  264120  |             AntiSpyware LLC              |
|       antispyware.sys       |  264110  |             AntiSpyware LLC              |
|       spywarebot.sys        |  264100  |                C-Netmedia                |
|          nomp3.sys          |  264000  |    Hamish Speirs （专用开发人员）     |
|        dlfilter.sys         |  263900  |            Starfield 软件            |
|          sifsp.sys          |  263800  |     Secure Islands Technologies LTD      |
|         DLFsFlt.sys         |  263700  |        CenterTools Software GmbH         |
|         SamKeng.sys         |  263600  |              Syvik 共同，ltd.              |
|           rml.sys           |  263500  |          Logis IT 服务 Gmbh           |
|         vfsmfd.sys          |  263410  |                Vontu Inc.                |
|         vfsmfd.sys          |  263400  |                Vontu Inc.                |
|        acfilter.sys         |  263300  |              Avalere, Inc.               |
|       psecfilter.sys        |  263200  |           MDI Laboratory, Inc.           |
|       SolRedirect.sys       |  263110  |             Soliton 系统              |
|         solitkm.sys         |  263100  |             Soliton 系统              |
|          ipcfs.sys          |  263000  |                 NetVeda                  |
|    netgateav\_access.sys    |  262910  |           NETGATE 技术。 s.r.o.           |
|     spyemrg\_access.sys     |  262900  |           NETGATE 技术。 s.r.o.           |
|         pxrmcet.sys         |  262800  |               Proxure Inc.               |
|        EgisTecFF.sys        |  262700  |           Egis 技术 inc.保留所有权利。           |
|         fgcpac.sys          |  262600  |           Fortres Grand corp.            |
|        saappctl.sys         |  262510  |           SecureAge 技术           |
|          sadlp.sys          |  262500  |           SecureAge 技术           |
|       CRExecPrev.sys        |  262410  |                Cybereason                |
|          PEG2.sys           |  262400  |                 PE 防护                 |
|       AdminRunFlt.sys       |  262300  |               Simon 贾维斯               |
|          wvscr.sys          |  262200  |          Chengdu Wei Tech Inc.           |
|       psepfilter.sys        |  262100  |            绝对软件             |
|        SAMDriver.sys        |  262000  |                峰会 IT                 |
|      wire_fsfilter.sys      |  261910  |             ThreatSpike 实验室             |
|   AMFileSystemFilter.sys    |  261900  |               AppSense Ltd               |
|          mtflt.sys          |  261880  |               mTalos Inc.                |
|         nxrmflt.sys         |  261680  |              NextLabs, Inc.              |
|         hdlpflt.sys         |  261200  |               McAfee Inc.                |
|        CCFFilter.sys        |  261160  |                Microsoft                 |
|         cbafilt.sys         |  261150  |                Microsoft                 |
| SmbBandwidthLimitFilter.sys |  261110  |                Microsoft                 |
|         DfsrRo.sys          |  261100  |                Microsoft                 |
|        DataScrn.sys         |  261000  |                Microsoft                 |
|         ldusbro.sys         |  260900  |               LANDesk inc.保留所有权利。               |
|    FileScreenFilter.sys     |  260800  |                 Veritas                  |
|        cpAcOnPnP.sys        |  260720  |               conpal GmbH                |
|        cpsgfsmf.sys         |  260710  |               conpal GmbH                |
|       psmmfilter.sys        |  260700  |                PolyServe                 |
|         pctefa.sys          |  260650  |            PC 工具 Pty. Ltd.            |
|        pctefa64.sys         |  260650  |            PC 工具 Pty. Ltd.            |
|        symefasi.sys         |  260610  |           Symantec Corporation           |
|         symefa.sys          |  260600  |                 Symantec                 |
|        symefa64.sys         |  260600  |                 Symantec                 |
|     aictracedrv\_cs.sys     |  260500  |              AI 咨询               |
|        DWFIxxxx.sys         |  260410  |         SciencePark Corporation          |
|        DWFIxxxx.sys         |  260400  |         SciencePark Corporation          |
|         FDriver.sys         |  260310  |                  Fox IT                  |
|          iqpk.sys           |  260300  |     Secure Islands Technologies LTD      |
|         VHDFlt.sys          |  260240  |                   Dell                   |
|         VHDFlt.sys          |  260230  |                   Dell                   |
|         VHDFlt.sys          |  260220  |                   Dell                   |
|         VHDFlt.sys          |  260210  |                   Dell                   |

## <a name="span-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspan240000---249999-fsfilter-quota-management"></a><span id="240000_-_249999__FSFilter_Quota_Management"></span><span id="240000_-_249999__fsfilter_quota_management"></span><span id="240000_-_249999__FSFILTER_QUOTA_MANAGEMENT"></span>240000 - 249999:FSFilter 配额管理


| 微筛选器      | 海拔高度 | 公司      |
|-----------------|----------|--------------|
| ntps\_qfs.sys   | 245100   | NTP Software |
| PSSFsFilter.sys | 245000   | PSS 系统  |
| Sptqmg.sys      | 245300   | Safend       |
| storqosflt.sys  | 244000   | Microsoft    |



## <a name="span-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspan220000---229999-fsfilter-system-recovery"></a><span id="220000_-_229999__FSFilter_System_Recovery"></span><span id="220000_-_229999__fsfilter_system_recovery"></span><span id="220000_-_229999__FSFILTER_SYSTEM_RECOVERY"></span>220000 - 229999:FSFilter 系统恢复


| 微筛选器          | 海拔高度 | 公司            |
|---------------------|----------|--------------------|
| file_protector.sys  | 227000   | Acronis            |
| fbwf.sys            | 226000   | Microsoft          |
| Klsysrec.sys        | 221500   | Kaspersky 实验室      |
| SFDRV.SYS           | 221400   | Utixo LLC          |
| sp\_prot.sys        | 221300   | Xacti Corporation  |
| nsfilep.sys         | 221200   | Netsupport Limited |
| syscow.sys          | 221100   | 系统确定 AB       |
| fsredir.sys         | 221000   | Microsoft          |



## <a name="span-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspan200000---209999-fsfilter-cluster-file-system"></a><span id="200000_-_209999__FSFilter_Cluster_File_System"></span><span id="200000_-_209999__fsfilter_cluster_file_system"></span><span id="200000_-_209999__FSFILTER_CLUSTER_FILE_SYSTEM"></span>200000 - 209999:FSFilter 群集文件系统


| 微筛选器          | 海拔高度 | 公司                  |
|---------------------|----------|--------------------------|
| CVCBT.sys           | 203400   | CommVault Systems, Inc.  |
| ResumeKeyFilter.sys | 202000   | Microsoft                |



## <a name="span-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspan180000---189999-fsfilter-hsm"></a><span id="180000_-_189999__FSFilter_HSM"></span><span id="180000_-_189999__fsfilter_hsm"></span><span id="180000_-_189999__FSFILTER_HSM"></span>180000 - 189999:FSFilter HSM


| 微筛选器                    | 海拔高度 | 公司                         |
|-------------------------------|----------|---------------------------------|
| wcifs.sys                     | 189900   | Microsoft                       |
| gvflt.sys                     | 189800   | Microsoft                       |
| Svfsf.sys                     | 186700   | Spharsoft 技术          |
| gwmemory.sys                  | 186600   | Macrotec LLC                    |
| cteraflt.sys                  | 186550   | CTERA Networks Ltd.             |
| dbx.sys                       | 186500   | Dropbox Inc.                    |
| quaddrasi.sys                 | 186400   | Quaddra 软件                |
| gdrive.sys                    | 186300   | Google                          |
| EaseTag.sys                   | 186200   | EaseVault Technologies Inc.     |
| hcminifilter.sys              | 186100   | 高兴云                     |
| PDFsFilter.sys                | 186000   | Raxco Sfotware                  |
| camino.sys                    | 185900   | CaminoSoft Corp                 |
| C2C\_AF1R.SYS                 | 185810   | C2C 系统                     |
| DFdriver.sys                  | 185800   | DataFirst Corporation           |
| amfadrv.sys                   | 185700   | Quest Software Inc.             |
| HSMdriver.sys                 | 185600   | Wim Vervoorn                    |
| kdfilter.sys                  | 185555   | Komprise Inc.                   |
| htdafd.sys                    | 185500   | 桥头软                 |
| SymHsm.sys                    | 185400   | Symantec                        |
| evmf.sys                      | 185100   | Symantec                        |
| otfilter.sys                  | 185000   | Overtone 软                   |
| ithsmdrv.sys                  | 184900   | IBM                             |
| MfaFilter.sys                 | 184800   | Waterford 技术          |
| SonyHsmMinifilter.sys         | 184700   | Sony Corporation                |
| acahsm.sys                    | 184600   | 自治 Corporation            |
| zlhsm.sys                     | 184500   | ZL 技术                 |
| Accesstracker.sys             | 183002   | Microsoft                       |
| Changetracker.sys             | 183001   | Microsoft                       |
| Fstier.sys                    | 183000   | Microsoft                       |
| hsmcdpflt.sys                 | 182700   | Metalogix                       |
| archivmgr.sys                 | 182690   | Metalogix                       |
| ntps\_oddm.sys                | 182600   | NTP Software                    |
| XDFileSys.sys                 | 182500   | XenData Limited                 |
| upmjit.sys                    | 182400   | Citrix Systems                  |
| AtmosFS.sys                   | 182310   | EMC Corporation                 |
| DxSpy.sys                     | 182300   | EMC Software Inc.               |
| car\_hsmflt.sys               | 182200   | Caringo, Inc.                   |
| BRDriver.sys                  | 182100   | BitRaider                       |
| BRDriver64.sys                | 182100   | BitRaider                       |
| autnhsm.sys                   | 182000   | 自治 Corporation            |
| cthsmflt.sys                  | 181970   | ComTrade                        |
| NxMini.sys                    | 181900   | NEXSAN                          |
| npfdaflt.sys                  | 181800   | Mimosa Systems Inc              |
| AppStream.sys                 | 181700   | AppStream, Inc.                 |
| HPEDpHsmX64.sys               | 181620   | Hewlett-Packard Co.，            |
| HPArcHsmX64.sys               | 181610   | Hewlett-Packard Co.，            |
| hphsmflt.sys                  | 181600   | Hewlett-Packard Co.，            |
| RepHsm.sys                    | 181500   | Double-Take Software, Inc.      |
| RepSIS.sys                    | 181490   | Double-Take Software            |
| SquashCompressionFsFilter.sys | 181410   | Squash 压缩              |
| GXHSM.sys                     | 181400   | Commvault 系统，Inc          |
| EdsiHsm.sys                   | 181300   | Enterprise Data Solutions, Inc. |
| BkfMap.sys                    | 181200   | 数据存储组              |
| hsmfilter.sys                 | 181100   | GRAU 数据存储可用性组            |
| mwi\_dmflt.sys                | 181000   | 月球漫步的例子 Univ                   |
| HcpAwfs.sys                   | 181960   | 人： Hitachi 数据系统            |
| sdrefltr.sys                  | 180950   | 人： Hitachi 数据系统            |
| fltasm.sys                    | 180900   | 全局 360                      |
| cnet\_hsm.sys                 | 180850   | Carroll Net                     |
| pntvolflt.sys                 | 180800   | 点软件和系统          |
| appxstrm.sys                  | 180710   | Microsoft                       |
| wimmount.sys                  | 180700   | Microsoft                       |
| dfmflt.sys                    | 180611   | Microsoft                       |
| hsmflt.sys                    | 180600   | Microsoft                       |
| dfsrflt.sys                   | 180500   | Microsoft                       |
| odphflt.sys                   | 180455   | Microsoft                       |
| cldflt.sys                    | 180451   | Microsoft                       |
| dedup.sys                     | 180450   | Microsoft                       |
| dfmflt.sys                    | 180410   | Microsoft                       |
| sis.sys                       | 180400   | Microsoft                       |
| rbt\_wfd.sys                  | 180300   | Riverbed 技术，Inc         |



## <a name="span-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspan170000---174999-fsfilter-imaging-ex-zip"></a><span id="170000_-_174999___FSFilter_Imaging__ex__.ZIP_"></span><span id="170000_-_174999___fsfilter_imaging__ex__.zip_"></span><span id="170000_-_174999___FSFILTER_IMAGING__EX__.ZIP_"></span>170000 - 174999:\*FSFilter 映像 (例如:。ZIP)


| 微筛选器        | 海拔高度 | 公司   |
|-------------------|----------|-----------|
| virtual\_file.sys | 172000   | Acronis   |
| wimFltr.sys       | 170500   | Microsoft |



## <a name="span-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspan160000---169999-fsfilter-compression"></a><span id="160000_-_169999__FSFilter_Compression"></span><span id="160000_-_169999__fsfilter_compression"></span><span id="160000_-_169999__FSFILTER_COMPRESSION"></span>160000 - 169999:FSFilter 压缩


| 微筛选器        | 海拔高度 | 公司              |
|-------------------|----------|----------------------|
| CmgFFC.sys        | 166000   | Credant 技术 |
| compress.sys      | 165000   | Microsoft            |
| cmpflt.sys        | 162000   | Microsoft            |
| IridiumIO.sys     | 161700   | Confio               |
| logcompressor.sys | 161600   | VelociSQL            |
| GcfFilter.sys     | 161500   | GemacmbH             |
| ssddoubler.sys    | 161400   | 思南 Karaca         |
| Sptcmp.sys        | 161300   | Safend               |
| wimfsf.sys        | 161000   | Microsoft            |
| GEFCMP.sys        | 160100   | Symantec             |



## <a name="span-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspan140000---149999-fsfilter-encryption"></a><span id="140000_-_149999__FSFilter_Encryption"></span><span id="140000_-_149999__fsfilter_encryption"></span><span id="140000_-_149999__FSFILTER_ENCRYPTION"></span>140000 - 149999:FSFilter 加密


| 微筛选器                  | 海拔高度 | 公司                               |
|-----------------------------|----------|---------------------------------------|
| EasyKryptMF.sys             | 149000   | SoftKrypt LLC                         |
| padlock.sys                 | 148910   | IntSoft Inc.                          |
| ffecore.sys                 | 148900   | Winmagic                              |
| klvfs.sys                   | 148810   | Kaspersky 实验室                         |
| Klfle.sys                   | 148800   | Kaspersky 实验室                         |
| ISIRM.sys                   | 148700   | 安装 ALPS 系统集成 CO。          |
| ASUSSecDrive.sys            | 148650   | ASUS                                  |
| ABFilterDriver.sys          | 148640   | AlertBoot                             |
| QDocumentFSF.sys            | 148630   | BicDroid Inc.                         |
| bfusbenc.sys                | 148620   | bitFence Inc.                         |
| sztgbfsf.sys                | 148610   | SaferZone Co.                         |
| mwIPSDFilter.sys            | 148600   | Egis 技术 inc.保留所有权利。                  |
| csccvdrv.sys                | 148500   | 计算机科学 Corporation         |
| aefs.sys                    | 148400   | Angelltech Corporation Xi'an          |
| IWCSEFlt.sys                | 148300   | InfoWatch                             |
| GDDmk.sys                   | 148250   | G Data Software AG                    |
| clcxcore.sys                | 148210   | 漂亮 Solutions Inc.                  |
| OrisLPDrv.sys               | 148200   | CGS 发布技术                   |
| nlemsys.sys                 | 148100   | NETLIB                                |
| prvflder.sys                | 148000   | Microsoft                             |
| ssefs.sys                   | 147900   | SecuLution GmbH                       |
| SePSed.sys                  | 147800   | 嗡嗡头，inc.                   |
| dlmfencx.sys                | 147700   | 数据加密 Ltd                   |
| psgcrypt.sys                | 147610   | Yokogawa R&L Corp                     |
| bbfsflt.sys                 | 147600   | Bloombase                             |
| qx10efs.sys                 | 147500   | Quixxant                              |
| MEfefs.sys                  | 147400   | Eruces Inc.                           |
| medlpflt.sys                | 147310   | 检查点软件 Technologies Ltd |
| dsfa.sys                    | 147308   | 检查点软件 Technologies Ltd |
| Snicrpt.sys                 | 147300   | Systemneeds, Inc                      |
| iCrypt.sys                  | 147200   | I-O DATA DEVICE, INC.                 |
| xdrmflt.sys                 | 147100   | bluefinsystems                        |
| dyFsFilter.sys              | 147000   | Scrypto 媒体                         |
| thinairwin.sys              | 146960   | 精简空气 Inc"                         |
| UcaDataMgr.sys              | 146950   | AppSense Ltd                          |
| zesocc.sys                  | 146900   | Novell                                |
| mfprom.sys                  | 146800   | McAfee Inc                            |
| MfeEEFF.sys                 | 146790   | McAfee                                |
| intefs.sys                  | 146700   | TianYu 软件                       |
| leofs.sys                   | 146600   | Leotech                               |
| autocryptater.sys           | 146500   | Richard Hagen                         |
| WavxDMgr.sys                | 146400   | Scott Cochrane                        |
| eedmkxp32.sys               | 146300   | Entrust                               |
| SbCe.sys                    | 146200   | SafeBoot                              |
| iSharedFsFilter             | 146100   | Packeteer Inc                         |
| dlrmenc.sys                 | 146010   | DESlock                               |
| dlmfenc.sys                 | 146000   | DESlock+                              |
| aksdf.sys                   | 145900   | 限于 Aladdin 知识系统             |
| DDSFilter.sys               | 145800   | WuHan Forworld 软件               |
| SecureShield.sys            | 145700   | HMI                                   |
| AifaFE.sys                  | 145600   | Alfa                                  |
| GBFsMf.sys                  | 145500   | GreenBorder                           |
| jmefs.sys                   | 145400   | 上海发电                         |
| emugufs.sys                 | 145333   | Emugu 安全 FS                       |
| VFDriver.sys                | 145300   | R 系统                             |
| EVSDecrypt64.sys            | 145230   | Fortium Technologies Ltd              |
| skycryptorencfs.sys         | 145220   | Onecryptor CJSC。                      |
| AisLeg.sys                  | 145210   | 有保证的信息安全          |
| windtalk.sys                | 145200   | Hyland 软件                       |
| TeamCryptor.sys             | 145190   | iTwin Pte。 Ltd.                       |
| CVDLP.sys                   | 145180   | CommVault Systems, Inc.               |
| 5nine.encryptor.sys         | 145170   | 5nine Software                        |
| ctpfile.sys                 | 145160   | 北京 Wondersoft 技术 Co.     |
| DPDrv.sys                   | 145150   | IBM 日本                             |
| tsdlp.sys                   | 145140   | Forware                               |
| KCDriver.sys                | 145130   | Tallegra Ltd                          |
| CmgFFE.sys                  | 145120   | Credant 技术                  |
| fgcenc.sys                  | 145110   | Fortres Grand corp.                   |
| sview.sys                   | 145100   | Cinea                                 |
| TalkeyFilterDriver.sys      | 145040   | myTALKEY s.r.o.                       |
| FedsFilterDriver.sys        | 145010   | 物理制作 Corp                  |
| stocc.sys                   | 145000   | Senforce 技术                 |
| SnEfs.sys                   | 144900   | Informzaschita                        |
| ewSecureDox                 | 144800   | Echoworx Corporation                  |
| osrdmk.sys                  | 144700   | OSR Open Systems Resources, Inc.      |
| uldcr.sys                   | 144600   | NCR 财务解决方案               |
| Tkefsxp.sys-32 位         | 144500   | INCA Internet Co., Ltd                |
| Tkefsxp64.sys - 64bit       | 144500   | INCA Internet Co., Ltd                |
| NmlAccf.sys                 | 144400   | NEC 系统技术，ltd.         |
| SolCrypt.sys                | 144300   | Soliton 系统 K.K.                  |
| IngDmk.sys                  | 144200   | Ingrian 网络，inc.                |
| llenc.sys                   | 144100   | SecureAxis Software                   |
| SecureData.sys              | 144030   | SecureAge 技术                  |
| lockcube.sys                | 144020   | SecureAge 技术 Pte Ltd          |
| sdmedia.sys                 | 144010   | SecureAge 技术                  |
| mysdrive.sys                | 144000   | SecureAge 技术                  |
| FileArmor.sys               | 143900   | 移动破解                          |
| VSTXEncr.sys                | 143800   | VIA Technologies, Inc.                |
| dgdmk.sys                   | 143700   | Verdasys Inc.                         |
| shandy.sys                  | 143600   | Safend ltd.                           |
| C2knet.sys                  | 143520   | Secuware                              |
| C2kdef.sys                  | 143510   | Secuware                              |
| ssfFS.sys                   | 143500   | SECUWARE S.L。                         |
| PISRFE.sys                  | 143400   | Jilin 大学 IT Co.               |
| bapfecre.sys                | 143300   | BitArmor Systems, Inc                 |
| KPSD.sys                    | 143200   | cihosoft                              |
| Fcfileio.sys                | 143100   | Brainzsquare，Co.Ltd.                |
| cpdrm.sys                   | 143000   | Pikewerks                             |
| vmfiltr.sys                 | 142900   | Vormetric Inc                         |
| VFSEnc.sys                  | 142811   | Symantec                              |
| pgpfs.sys                   | 142810   | Symantec                              |
| fencry.sys                  | 142800   | Symantec                              |
| TmFileEncDmk.sys            | 142700   | Trend Micro Inc                       |
| cpefs.sys                   | 142600   | 加密 Pro                            |
| dekfs.sys                   | 142500   | KasherLab co.ltd                     |
| qlockfilter.sys             | 142400   | Binqsoft Inc.                         |
| RRFilterDriverStack\_d3.sys | 142300   | 合理的保留期                    |
| cve.sys                     | 142200   | 绝对软件 corp.               |
| spcflt.sys                  | 142100   | FUJITSU BSC inc.保留所有权利。                      |
| ldsecusb.sys                | 142000   | LANDesk inc.保留所有权利。                          |
| fencr.sys                   | 141900   | SODATSW spol。 s.r.o.                  |
| RubiFlt.sys                 | 141800   | 人： Hitachi                               |
| CovertxFilter.sys           | 141700   | Covertix                              |
| mfild.sys                   | 141660   | Penta 安全系统                |
| TypeSquare.sys              | 141620   | Morisawa inc。                         |
| xbdocfilter.sys             | 141610   | Zrxb                                  |
| EVSDecrypt32.sys            | 141600   | Fortium Technologies Ltd              |
| EVSDecrypt64.sys            | 141600   | Fortium Technologies Ltd              |
| EVSDecryptia64.sys          | 141600   | Fortium Technologies Ltd              |
| afdriver.sys                | 141500   | ATUS 技术 LLC                   |
| TrivalentFSFltr.sys         | 141430   | 网络依赖                         |
| CmdMnEfs.sys                | 141420   | Comodo 安全                       |
| DWENxxxx.sys                | 141410   | SciencePark Corporation               |
| DWENxxxx.sys                | 141400   | SciencePark Corporation               |
| hdFileSentryDrv32.sys       | 141300   | Heilig 防御                        |
| hdFileSentryDrv64.sys       | 141300   | Heilig 防御                        |
| Filecrypt.sys               | 141100   | Microsoft                             |
| encrypt.sys                 | 141010   | Microsoft                             |
| swapBuffers.sys             | 141000   | Microsoft                             |



## <a name="span-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspan130000---139999-fsfilter-virtualization"></a><span id="130000_-_139999__FSFilter_Virtualization"></span><span id="130000_-_139999__fsfilter_virtualization"></span><span id="130000_-_139999__FSFILTER_VIRTUALIZATION"></span>130000 - 139999:FSFilter 虚拟化


| 微筛选器             | 海拔高度 | 公司                       |
|------------------------|----------|-------------------------------|
| Klvirt.sys             | 138100   | Kaspersky 实验室                 |
| GetSAS.sys             | 138040   | SAS Institute Inc             | 
| rqtNos.sys             | 138030   | ReaQta ltd.                   |
| HIPS64.sys             | 138020   | Recrypt LLC                   |
| frxdrv.sys             | 138010   | FSLogix                       |
| vzdrv.sys              | 138000   | Altiris                       |
| sffsg.sys              | 137990   | 海星存储 Corp         | 
| AppStream.sys          | 137920   | Symantec Corporation          |
| boxifier.sys           | 137910   | Kenubi                        |
| xorw.sys               | 137900   | CA (XOsoft)                   |
| ctlua.sys              | 137800   | SurfRight B.V.                |
| fgccow.sys             | 137700   | Fortres Grand corp.           |
| aswSnx.sys             | 137600   | ALWIL 软件                |
| AppIsoFltr.sys         | 137500   | 内核驱动程序                |
| ptcvfsd.sys            | 137400   | PTC                           |
| BDSandBox.sys          | 137300   | BitDefender SRL               |
| sxfpss-virt.sys        | 137200   | Skanix AS                     |
| DKRtWrt.sys            | 137100   | 为 diskeeper Corporation         |
| ivm.sys                | 137000   | RingCube 技术         |
| ivm.sys                | 136990   | Citrix Systems                |
| dtiof.sys              | 136900   | Instavia Software Inc.        |
| NxTopCP.sys            | 136800   | 虚拟计算机的消息 inc.保留所有权利。        |
| svdriver.sys           | 136700   | VMware, Inc.                  |
| unifltr.sys            | 136600   | Unidesk                       |
| unirsd.sys             | 136600   | Unidesk                       | 
| unidrive.sys （重命名） | 136600   | Unidesk                       |
| ive.sys                | 136500   | TrendMicro Inc.               |
| odamf.sys              | 136450   | Sony Corporation              |
| SrMxfMf.sys            | 136440   | Sony Corporation              |
| pszmf.sys              | 136430   | Sony Corporation              |
| sxsudfmf.sys           | 136410   | Sony Corporation              |
| vfammf.sys             | 136400   | Sony Corporation              |
| VHDFlt.sys             | 136240   | Dell                          |
| VHDFlt.sys             | 136230   | Dell                          |
| VHDFlt.sys             | 136220   | Dell                          |
| VHDFlt.sys             | 136210   | Dell                          |
| ncfsfltr.sys           | 136200   | NComputing                    |
| cmdguard.sys           | 136100   | COMODO 安全解决方案 Inc |
| hpfsredir.sys          | 136000   | HP                            |
| svhdxflt.sys           | 135100   | Microsoft                     |
| luafv.sys              | 135000   | Microsoft                     |
| ivm.sys                | 134000   | RingCube 技术         |
| ivm.sys                | 133990   | Citrix Systems                |
| frxdrvvt.sys           | 132700   | FSLogix Inc.                  | 
| Stcvhdmf.sys           | 132600   | StorageCraft 技术 Corp        |
| pfmfs_???.sys          | 132600   | Pismo Technic Inc.            | 
| appdrv01.sys           | 132500   | 保护技术         |
| virtual\_file.sys      | 132400   | Acronis                       |
| pdiFsFilter.sys        | 132300   | Proximal 数据 inc.保留所有权利。            |
| avgvtx86.sys           | 132200   | AVG 技术 CZ           |
| avgvtx64.sys           | 132200   | AVG 技术 CZ           |
| DataNet\_Driver.sys    | 132100   | AppSense Ltd                  |
| EgenPage.sys           | 132000   | Egenera, Inc.                 |
| unidrive.sys-old       | 131900   | Unidesk                       |
| ivm.sys.old            | 131800   | RingCube 技术         |
| XiaobaiFsR.sys         | 131710   | 深圳 UNNOO LTD            |
| XiaobaiFs.sys          | 131700   | 深圳 UNNOO LTD            |
| iotfsflt.sys           | 131600   | IO 涡轮机 Inc                |
| mhpvfs.sys             | 131500   | Wunix Limited                 |
| svdriver.sys           | 131400   | SnapVolumes                   |
| Sptvrt.sys             | 131300   | Safend                        |
| aicvirt.sys            | 131200   | AI 咨询                 |
| sfo.sys                | 130100   | Microsoft                     |
| DeVolume.sys           | 130000   | Microsoft                     |



## <a name="span-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspan120000---129999-fsfilter-physical-quota-management"></a><span id="120000_-_129999__FSFilter_Physical_Quota_Management"></span><span id="120000_-_129999__fsfilter_physical_quota_management"></span><span id="120000_-_129999__FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>120000 - 129999:FSFilter 物理配额管理


| 微筛选器   | 海拔高度 | 公司       |
|--------------|----------|---------------|
| quota.sys    | 125000   | Microsoft     |
| qafilter.sys | 124000   | Veritas       |
| DroboFlt.sys | 123900   | 数据机器人 |



## <a name="span-id100000-109999fsfilterfilteropenfilespanspan-id100000-109999fsfilterfilteropenfilespanspan-id100000-109999fsfilterfilteropenfilespan100000---109999-fsfilter-filter-open-file"></a><span id="100000_-_109999__FSFilter_Filter_Open_File"></span><span id="100000_-_109999__fsfilter_filter_open_file"></span><span id="100000_-_109999__FSFILTER_FILTER_OPEN_FILE"></span>100000 - 109999:FSFilter 筛选器打开的文件


| 微筛选器      | 海拔高度 | 公司                |
|-----------------|----------|------------------------|
| insyncmf.sys    | 105000   | InSync                 |
| SPILock8.sys    | 100900   | Software Pursuits Inc. |
| Klbackupflt.sys | 100800   | Kaspersky              |
| repkap          | 100700   | 视觉解决方案       |
| symrg.sys       | 100600   | Symantec               |
| adsfilter.sys   | 100500   | PolyServ               |



## <a name="span-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspan80000---89999-fsfilter-security-enhancer"></a><span id="80000_-_89999__FSFilter_Security_Enhancer"></span><span id="80000_-_89999__fsfilter_security_enhancer"></span><span id="80000_-_89999__FSFILTER_SECURITY_ENHANCER"></span>80000 - 89999:FSFilter 安全不得不


| 微筛选器              | 海拔高度 | 公司                                  |
|-------------------------|----------|------------------------------------------|
| dsbwnck.sys             | 88000    | 简单的解决方案 inc.保留所有权利。                       |     
| rsbfsfilter.sys         | 87800    | Corel Corporation                        |
| hsmltflt.sys            | 87720    | 人： Hitachi Solutions                        |
| hssfflt.sys             | 87710    | 人： Hitachi Solutions                        |
| acmnflt.sys             | 87708    | 人： Hitachi Solutions                        |
| ACSKFFD.sys             | 87700    | 人： Hitachi Solutions                        |
| MyDLPMF.sys             | 87600    | Comodo Group Inc.                        |
| ScuaRaw.sys             | 87500    | SCUA Segurança da Informação             |
| HDSFilter.sys           | 87400    | NeoAutus 自动化系统               |
| ikfsmflt.sys            | 87300    | IronKey Inc.                             |
| Klsec.sys               | 87200    | Kaspersky 实验室                            |
| XtimUSBFsFilterDrv.sys  | 87190    | Dalian CP-SDT Ltd                        |
| RGFLT_FM.sys            | 87180    | Hauri.inc                                |
| flockflt.sys            | 87170    | Ahranta                                  |
| ZdCore.sys              | 87160    | Zends 技术解决方案            |
| dcrypt.sys              | 87150    | ReactOS Foundation                       |
| hpradeo.sys             | 87140    | Pradeo                                   |
| SDFSAGDRV.SYS           | 87130    | 安装 ALPS 系统集成 CO。             |
| SDFSDEVFDRV.SYS         | 87120    | 安装 ALPS 系统集成 CO。             |
| SDIFSFDRV.SYS           | 87110    | 安装 ALPS 系统集成 CO。             |
| SDFSFDRV.SYS            | 87100    | 安装 ALPS 系统集成 CO。             |
| HHRRPH.sys              | 87010    | H+H Software GmbH                        |
| HHVolFltr.sys           | 87000    | H+H Software GmbH                        |
| SbieDrv.sys             | 86900    | Sandboxie L.T.D                          |
| assetpro.sys            | 86800    | pyaprotect.com                           |
| dlp.sys                 | 86700    | Tellus Software AS                       |
| eps.sys                 | 86600    | Lumension 安全                       |
| RapportPG64.sys         | 86500    | Trusteer                                 |
| amminifilter.sys        | 86400    | AppSense                                 |
| Sniflt.sys              | 86300    | Systemneeds, Inc                         |
| SecFile.sys             | 86200    | 安全设计 Inc.                    |
| philly.sys              | 86110    | triCerat Inc.                            |
| reggy.sys               | 86100    | triCerat Inc.                            |
| cygfilt.sys             | 86000    | Livegrid Incorporated                    |
| prelaunch.sys           | 85900    | D3L                                      |
| csareg.sys              | 85810    | Cisco 系统                            |
| csaenh.sys              | 85800    | Cisco 系统                            |
| asEpsDrv.sys            | 85750    | ASHINI 有限公司                          |
| CIDACL.sys              | 85700    | GE 航空 (数字系统 Germantown) |
| CVDLP.sys               | 85610    | CommVault Systems, Inc.                  |
| QGPEFlt.sys             | 85600    | Quest Software                           |
| Drveng.sys              | 85500    | CA                                       |
| vracfil2.sys            | 85400    | HAURI                                    |
| TFsDisk.sys             | 85300    | Teruten                                  |
| rcMiniDrv.sys           | 85200    | REDGATE CO.，LTD.                         | 
| SnMc5xx.sys             | 85100    | Informzaschita                           |
| FSPFltd.sys             | 85010    | Alfa                                     |
| AifaFFP.sys             | 85000    | Alfa                                     |
| EsAccCtlFE.sys          | 84901    | EgoSecure GmbH                           |
| DpAccCtl.sys            | 84900    | Softbroker GmbH                          |
| privman.sys             | 84800    | BeyondTrust                              |
| eumntvol.sys            | 84700    | Eugrid Inc                               |
| SoloEncFilter.sys       | 84600    | Soliton 系统                          |
| sbfilter.sys            | 84500    | UC4 软件                              |
| cposfw.sys              | 84450    | 检查点软件 Technologies ltd.   |
| vsdatant.sys            | 84400    | 区域实验室 LLC                            |
| SePnet.sys              | 84350    | 嗡嗡头，inc.                      |
| SePuld.sys              | 84340    | 嗡嗡头，inc.                      |
| SePpld.sys              | 84330    | 嗡嗡头，inc.                      |
| SePfsd.sys              | 84320    | 嗡嗡头，inc.                      |
| SePwld.sys              | 84310    | 嗡嗡头，inc.                      |
| SePprd.sys              | 84300    | 嗡嗡头，inc.                      |
| InPFlter.sys            | 84200    | 嗡嗡头，inc.                      |
| CProCtrl.sys            | 84100    | 加密 Pro                               |
| spyshelter.sys          | 84000    | Datpol                                   |
| clpinspprot.sys         | 83900    | 信息技术公司 ltd.      |
| uvmfsflt.sys            | 83376    | NEC Corporation                          |
| dguard.sys              | 82300    | Dmitry Varshavsky                        |
| NSUSBStorageFilter.sys  | 82200    | NetSupport Ltd                           |
| RMSEFFMV.SYS            | 82100    | CJSC Returnil 软件                   |
| BoksFLAC.sys            | 82000    | Fox 技术                         |
| cpAcOnPnP.sys           | 81910    | conpal GmbH                              |
| cpsgfsmf.sys            | 81900    | conpal GmbH                              |
| ndevsec.sys             | 81800    | Norman ASA                               |
| ViewIntus_RTDG.sys      | 81700    | Pentego Technologies Ltd                 |
| airlock.sys             | 81630    | 太空飞船数字 Pty Ltd                  |
| zam.sys                 | 81620    |                                          |
| ANXfsm.sys              | 81610    | Arcdo                                    |
| CDrSDFlt.sys            | 81600    | Arcdo                                    |
| crnselfdefence32.sys    | 81500    | Coranti                                  |
| crnselfdefence64.sys    | 81500    | Coranti                                  |
| zlock_drv.sys           | 81400    | SecurIT                                  |
| f101fs.sys              | 81300    | Fortres Grand corp.                      |
| sysgar.sys              | 81200    | 核心数据恢复                     |
| EmbargoM.sys            | 81100    | ScriptLogic                              |
| ngssdef.sys             | 81050    | Wontok                                   |
| fsds2a.sys              | 81000    | Splitstreem ltd.                         |
| csacentr.sys            | 80900    | Cisco 系统                            |
| ScvFLT50.sys            | 80850    | Secuve Ltd                               |
| paritydriver.sys        | 80800    | Bit9, Inc.                               |
| nkfsprot.sys            | 80710    | Konneka                                  |
| nkprot.sys              | 80700    | KONNEKA 信息技术         |
| acpadlock.sys           | 80691    | IntSoft Co                               |
| ksmf.sys                | 80690    | IntSoft Co                               |
| im.sys                  | 80680    | CrowdStrike                              |
| SophosED.sys            | 80670    | Sophos                                   |



## <a name="span-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspan60000---69999-fsfilter-copy-protection"></a><span id="60000_-_69999__FSFilter_Copy_Protection"></span><span id="60000_-_69999__fsfilter_copy_protection"></span><span id="60000_-_69999__FSFILTER_COPY_PROTECTION"></span>60000 - 69999:FSFilter 复制保护


| 微筛选器             | 海拔高度 | 公司                                 |
|------------------------|----------|-----------------------------------------|
| CkProcess.sys          | 66100    | KASHU 系统设计 INC.保留所有权利。                |
| dlmfprot.sys           | 66000    | 数据加密 Sys                        |
| baprtsef.sys           | 65700    | BitArmor Systems, Inc                   |
| sxfpss.sys             | 65600    | Skanix AS                               |
| rgasdev.sys            | 65500    | Macrovision                             |
| SkyFPDrv.sys           | 65410    | 天空 Co.，Ltd.                            | 
| SkyWPDrv.sys           | 65400    | 天空 Co.，Ltd.                            |
| SnEraser.sys           | 65300    | Informzaschita                          |
| vfilter.sys            | 65200    | RSJ Software GmbH                       |
| COGOFlt32.sys          | 65100    | Fortium Technologies Ltd                |
| COGOFlt64.sys          | 65100    | Fortium Technologies Ltd                |
| COGOFLTia64.sys        | 65100    | Fortium Technologies Ltd                |
| scrubber.sys           | 65000    | Microsoft                               |
| BRDriver.sys           | 64000    | BitRaider LLC                           |
| BRDriver64.sys         | 64000    | BitRaider LLC                           |
| LibertyFSF.sys         | 62300    | Bayalink 解决方案 Co                   |
| axfsdrv2.sys           | 62100    | Axence 软件                         |
| sds.sys                | 62000    | 出口软件                         |
| TotalSystemAuditor.sys | 61600    | ANRC LLC                                |
| MBAMApiary.sys         | 61500    | Malwarebytes corp.                      |
| WA\_FSW.sys            | 61400    | Programas Administracion y Mejoramiento |
| ViewIntus\_RTAS        | 61300    | Pentego 技术                    |
| tffac.sys              | 61200    | Toshiba Corporation                     |
| tccp.sys               | 61100    | TrusCont Ltd                            |
| KomFS.sys              | 61000    | KOM 网络                            |



## <a name="span-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspan40000---49999-fsfilter-bottom"></a><span id="40000_-_49999__FSFilter_Bottom"></span><span id="40000_-_49999__fsfilter_bottom"></span><span id="40000_-_49999__FSFILTER_BOTTOM"></span>40000 - 49999:FSFilter 底部


| 微筛选器          | 海拔高度 | 公司            |
|---------------------|----------|--------------------|
| DLDriverMiniFlt.sys | 47200    | DeviceLock Inc     |
| hsmltlib.sys        | 47110    | 人： Hitachi Solutions  |
| hskdlib.sys         | 47100    | 人： Hitachi Solutions  | 
| acmnlib.sys         | 47090    | 人： Hitachi Solutions  |
| aictracedrv\_b.sys  | 47000    | AI 咨询      |
| hhdcfltr.sys        | 46900    | Seagate 技术 |
| Npsvctrig.sys       | 46000    | Microsoft          |
| fileinfo            | 45000    | Microsoft          |
| klvfs.sys           | 44900    | Kaspersky 实验室      |
| rsfxdrv.sys         | 41000    | Microsoft          |
| defilter.sys        | 40900    | Microsoft          |
| AppVVemgr.sys       | 40800    | Microsoft          |
| wof.sys             | 40700    | Microsoft          |



## <a name="span-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspan20000---29999-fsfilter-system"></a><span id="20000_-_29999__FSFilter_System"></span><span id="20000_-_29999__fsfilter_system"></span><span id="20000_-_29999__FSFILTER_SYSTEM"></span>20000 - 29999:FSFilter 系统


无。








