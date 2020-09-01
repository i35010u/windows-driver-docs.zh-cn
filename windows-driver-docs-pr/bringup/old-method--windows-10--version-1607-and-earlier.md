---
title: 旧方法-Windows 10 版本1607及更早版本
description: 旧方法-Windows 10 版本1607及更早版本
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6432cf703dcd47a2d3d503d1c520201b64668a24
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188085"
---
# <a name="old-method---windows-10-version-1607-and-earlier"></a>旧方法-Windows 10 版本1607及更早版本

在将 Windows 7 (到 Windows 10) 的升级方案中，技术人员需要将操作系统和固件从 Windows 7 SPn 旧版 boot + CSM 更改为 Win10 UEFI-CSM (减去 CSM) ，并具有 Windows 7 SPn x64 安装媒体。

此过程可能如下所示 (更详细) ：

1. 咨询此固件或主板可用的 OEM 安全选项。 某些固件或主板上并不是所有安全选项都可用。

2. 备份整个主启动磁盘 (上计划保存) 的所有数据。

    > [!NOTE]
    > 建议创建映像或具有 OEM 恢复介质。

3. 创建可启动的 x64 WinPE USB 闪存驱动器 (UFD) 或 CD/DVD。

4. 重新启动到固件用户界面 (UI) 并切换设置以启动到 UEFI (如果需要重新启动到 Win7，你将需要启用了 CSM) 。

5. 若要启动到备用启动设备) ，请在 USB/CD/DVD 设备上启动到 WinPE (**安全启动** 。

6. 使用 Diskpart.exe 擦除干净的主启动磁盘。

    > [!NOTE]
    > 如果存在多个磁盘，请在清理磁盘之前验证磁盘0是否为主启动设备，因为此过程会擦除磁盘上的所有数据。

7. 此时有几个选项，IT 人员可能需要联系系统 OEM 以获取特定说明/配置选项。

    a.  插入干净的安装介质并运行 setup.exe。 安装过程可能会检测 CSM 并在传统启动/BIOS 模式下重新安装。

    b.  在步骤5中，仍处于 Diskpart.exe 选择 "主启动磁盘"，运行 "转换 GPT"

      - 插入安装媒体、重新启动并完成安装。 如果遇到一条错误消息，其中包含类似文本 "无法安装到选定设备" 或 "不支持磁盘格式"，则启动设备将检测 CSM，并尝试启动到旧式启动 MBR 方法。

      - 或者，按照步骤为 UEFI 启动方法手动配置 GPT 磁盘。 查看 [建议的基于 UEFI 的磁盘分区配置](/previous-versions/windows/it-pro/windows-7/dd744301(v=ws.10)) ，然后通过 setup.exe 面向第三个分区来运行。

8. 在系统上安装 Windows 7 并运行 (后，你可能需要修补到最新版本) 然后升级到 Windows 10。

9. 安装并修补 Windows 10 后，请使用禁用 CSM 进行测试，并与制造商合作，启用此系统上可用的安全选项。

    > [!NOTE]
    > 在某些情况下，固件具有特定于 UEFI 的启动选项。 例如，选择一个) 启动选项或 b) UEFI 启动选项。

## <a name="related-resources"></a>相关资源

[建议的基于 UEFI 的磁盘分区配置](/previous-versions/windows/it-pro/windows-7/dd744301(v=ws.10))