---
title: 在设备安装和驱动程序更新期间避免重启
description: 在设备安装和驱动程序更新期间避免系统重启
ms.assetid: b30c9e5f-85af-4e7f-81aa-67fe2df8a178
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 004d3f794cea8e65df1fa7abe9c3ee403914f847
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380347"
---
# <a name="avoiding-system-restarts-during-device-installations-and-driver-updates"></a>在设备安装和驱动程序更新期间避免系统重启


若要在设备安装期间避免系统重启，请使用以下规则：

-   永远不会使用**重新启动**或**重新启动**中的条目[ **INF DDInstall 部分**](inf-ddinstall-section.md)。 这些指令最初为提供与 Windows 兼容性的 9 倍 / 我，因此不应为 Windows 2000 和更高版本的 Windows。

-   执行不使用 COPYFLG_FORCE_FILE_IN_USE 或 COPYFLG_REPLACE_BOOT_FILE 标志与[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)，除非绝对必要。

-   将新文件的名称分配给类安装程序或辅助安装程序或服务 DLL 的每个新版本。 如果正在使用中的较旧版本，这样可避免系统重启的需要。 （事实上，如果新的文件名称不用于安装程序更新后的类或类共同安装程序，这些新文件将不会用于安装。）

-   若要更新的设备驱动程序，请执行下列出的规则[更新驱动程序文件](updating-driver-files.md)。

## <a name="minimizing-restarts-when-updating-file-backed-drivers"></a>更新支持文件的驱动程序时尽量减少重新启动


在 Windows 10 之前所有内核模式驱动程序已由系统分页文件提供都支持。 因此，驱动程序二进制文件可能会覆盖磁盘上运行该驱动程序时，甚至。

若要提高性能，从 Windows 10 开始大多数非引导启动驱动程序改为受支持驱动程序二进制文件在磁盘上。

驱动程序现在是文件备份的启动类型包括：

-   SERVICE_SYSTEM_START (0x00000001)
-   SERVICE_AUTO_START (0x00000002)
-   SERVICE_DEMAND_START (0x00000003)

启动开始驱动程序将继续由分页文件支持。

若要更新的支持文件的驱动程序，请使用以下最佳实践。 否则，更新可能需要两次重启，要替换的文件和第二个要加载新版本的驱动程序的一个。

如果使用的 INF 文件，请按照下列步骤：

1.  修改驱动程序 INF 文件的**CopyFiles**要使用的部分**COPYFLG_IN_USE_RENAME**，按如下所示：

    ```cpp
    [MyDriver_Install.NT]
    CopyFiles=MyDriverCopy
     
    [MyDriverCopy]
    MyDriver.sys,,,0x00004000  ; COPYFLG_IN_USE_RENAME
    ```

    如果使用此标志，Windows 将尝试替换为磁盘上的驱动程序文件。 有关详细信息，请参阅[INF CopyFiles 指令](inf-copyfiles-directive.md)。

2.  如果 INF 适用的即插即用驱动程序，请在设备安装 Windows 尝试卸载正在运行的驱动程序并重新启动才能选取新版本的驱动程序使用它的设备。 如果失败，设备安装指示应重新启动系统。
3.  如果 INF 即插即用驱动程序并不使用一种方法，如[ **InstallHInfSection** ](https://msdn.microsoft.com/library/windows/desktop/aa376957)处理 INF，则手动停止并重新启动该驱动程序：
    -   关闭所有打开的句柄驱动程序，然后停止驱动程序使用以下项之一：

        -   **sc.exe stop** *&lt;mydriver&gt;*
        -   **ControlService(SERVICE_CONTROL_STOP)**

        有关详细信息，请参阅[ **control 服务函数**](https://msdn.microsoft.com/library/windows/desktop/ms682108)。

如果不使用 INF 文件，使用以下步骤：

1.  停止该驱动程序，如上文所述。 替换为新旧驱动程序二进制文件。
2.  如果您不能停止该驱动程序，重命名现有文件，将新文件复制到的位置，并设置现有文件以在将来删除 (例如，使用[ **MoveFileEx** ](https://msdn.microsoft.com/library/windows/desktop/aa365240)与**MOVEFILE_DELAY_UNTIL_REBOOT**标志)。 为了开始使用新版本的驱动程序，系统将需要重新启动。

## <a name="related-topics"></a>相关主题


[文件备份和支持页的文件部分](https://msdn.microsoft.com/library/windows/hardware/ff545754)

[加载驱动程序时由什么决定](https://msdn.microsoft.com/library/windows/hardware/ff557272)

 

 






