---
title: 驱动程序安装
description: 此 SDK 中提供的打印驱动程序是实验性 3D 打印机设备驱动程序仍处于开发阶段。
ms.assetid: 8A13CD6F-DF82-4353-ADE9-06989F83BC87
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d6617e65e995a45353bb0a8aa178dbfa2f95607
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325775"
---
# <a name="driver-installation"></a>驱动程序安装


> [!NOTE]
> 3D 打印 SDK 中提供的打印驱动程序是实验性 3D 打印机设备驱动程序仍处于开发阶段。

## <a name="driver-installation"></a>驱动程序安装


若要安装打印机，请使用以下安装说明：

- 3D 打印机是否实现 Microsoft 操作系统描述符 3DPRINT ("MS\_COMP\_3DPRINT") 是一个支持供应商 ID (VID) 或产品 ID (PID) 组合在 MS3DPrintUSB.inf 文件中，按照中的步骤 /*自动通过即插即用驱动程序的安装*下面一节。

- 如果 3D 打印机是实验性或在开发过程中，按照中的步骤*手动安装驱动程序*以下部分来打印到现有的 COM 端口或 G 代码打印到文件。

MS_COMP_3DPRINT 的信息，请参阅[3D 打印机的 Microsoft 标准驱动程序的入门指南-](https://docs.microsoft.com/windows-hardware/drivers/3dprint/microsoft-standard-driver-for-3d-printers-)。

有关操作系统描述符的详细信息，请参阅[USB 设备的 Microsoft 操作系统描述符](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)。

### <a name="automatic-installation-of-the-driver-via-pnp"></a>通过即插即用驱动程序的自动安装

1.  如果设备不具有 MSO 描述符或支持的硬件 ID (VID/PID)，将新的 VID/PID 组合添加到 MS3DPrintUSB\_{体系结构}\\MS3DPrintUSB.inf 文件和使用高级的设置和驱动程序的重启 Windows签名已禁用。 暂时，并出于开发目的，仅应使用此选项。

2.  从提升的命令提示符中执行这两个命令：

    ```console
    pnputil -a {PathToSDK}\Bin\MS3DPrintUSB_{architecture}\MS3DPrintUSB.inf
    pnputil -a {PathToSDK}\Bin\RenderFilters_{architecture}\MS3DPrinter.inf
    ```

3.  插入 USB 串行设备。 一个新**泛型 3D 打印机**设备应安装下**设备和打印机**。

### <a name="install-the-driver-manually"></a>手动安装驱动程序

1.  搜索中 printmanagement.msc **Cortana**。

    ![打印管理](images/g-code-1.png)

2.  展开**打印服务器**，展开你的计算机的名称，右键单击**驱动程序**，然后选择**添加驱动程序...**.

    ![打印管理对话框](images/g-code-2.png)

3.  单击**下一步**，选择 **(x64)**，单击**下一步**，然后单击**磁盘安装**。

4.  导航到 RenderFiltersV4\_x64 文件夹中，选择 MS3DPrinter.inf，然后单击**确定**。

5.  单击**确定**，单击**下一步**，然后单击**完成**。

6.  从**Windows 启动**，类型**设备和打印机**。

7.  单击**添加打印机**。

    ![添加打印机](images/g-code-3.png)

8.  选择**我想的打印机未列出**。

    ![添加设备](images/g-code-4.png)

9.  选择**使用手动设置添加本地打印机或网络打印机**，然后单击**下一步**。

    ![使用手动设置添加本地打印机或网络打印机](images/g-code-5.png)

10. 选择**创建新的端口**，然后选择**3D 端口**端口类型，然后单击**下一步**。

    ![创建新的端口](images/g-code-6.png)

11. 输入端口名称，然后单击**确定**。

    ![输入端口名称](images/g-code-7.png)

12. 单击**从磁盘安装...**.

    ![从磁盘安装...](images/g-code-8.png)

13. 浏览到泛型的 3D 打印驱动程序二进制包从 SDK 单击**确定**。

14. 单击“下一步” 。

    ![安装打印机驱动程序](images/g-code-9.png)

15. 如果您愿意，可以更改此处的 3D 打印机名称 （它将显示在打印机用户界面），然后单击**下一步**，然后单击**确定**以允许要以管理员身份运行的命令。

    ![键入打印机名称](images/g-code-10.png)

16. 安装完成后，单击**完成**。








