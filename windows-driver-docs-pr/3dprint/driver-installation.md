---
title: 驱动程序安装
description: 此 SDK 中提供的打印驱动程序是一个仍在开发中的实验性三维打印机设备驱动程序。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3e3d28555aafe1a6fbaf668227c7b3cf7aa6f1a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783649"
---
# <a name="driver-installation"></a>驱动程序安装


> [!NOTE]
> 3D 打印 SDK 中提供的打印驱动程序是一个仍在开发中的实验性三维打印机设备驱动程序。

## <a name="driver-installation"></a>驱动程序安装


若要安装打印机，请使用以下安装说明：

- 如果3D 打印机实现了 Microsoft OS 描述符 3DPRINT ( "MS \_ COMP \_ 3DPRINT" ) 或者是受支持的供应商 ID 之一 (VID) /Product 文件中的 ID (PID) 组合，请按照下面的 " *通过 PnP 自动安装驱动程序* " 部分中的步骤进行操作。

- 如果3D 打印机是实验性或正在开发，请按照下面的 " *手动安装驱动程序"* 部分中的步骤进行操作，以打印到现有的 COM 端口或将 G 代码打印到文件。

有关 MS_COMP_3DPRINT 的信息，请参阅 [入门指南-适用于3D 打印机的 Microsoft 标准驱动程序](./microsoft-standard-driver-for-3d-printers-.md)。

有关操作系统描述符的详细信息，请参阅 [适用于 USB 设备的 MICROSOFT OS 描述符](../usbcon/microsoft-defined-usb-descriptors.md)。

### <a name="automatic-installation-of-the-driver-via-pnp"></a>通过 PnP 自动安装驱动程序

1.  如果设备没有 MSO.DLL 描述符或受支持的硬件 ID (VID/PID) ，请将新的 VID/PID 组合添加到 MS3DPrintUSB \_ {体系结构} \\ MS3DPrintUSB 文件，并在禁用高级设置和驱动程序签名的情况下重启 Windows。 此选项只应暂时用于开发目的。

2.  在提升的命令提示符下执行以下两个命令：

    ```console
    pnputil -a {PathToSDK}\Bin\MS3DPrintUSB_{architecture}\MS3DPrintUSB.inf
    pnputil -a {PathToSDK}\Bin\RenderFilters_{architecture}\MS3DPrinter.inf
    ```

3.  插入 USB 串行设备。 应该在 "**设备和打印机**" 下安装新的 **一般3d 打印机** 设备。

### <a name="install-the-driver-manually"></a>手动安装驱动程序

1.  搜索 **Cortana** 中的 printmanagement.msc。

    ![打印管理](images/g-code-1.png)

2.  展开 " **打印服务器**"，展开您的计算机的名称，右键单击 " **驱动程序**"，然后选择 " **添加驱动程序 ...**"。

    !["打印管理" 对话框](images/g-code-2.png)

3.  单击 "**下一步**"，选择 **(x64)**，单击 "**下一步**"，然后单击 "**从磁盘安装**

4.  导航到 RenderFiltersV4 \_ x64 文件夹，选择 "MS3DPrinter"，然后单击 **"确定"**。

5.  单击 **"确定"**，单击 " **下一步**"，然后单击 " **完成**"

6.  从 **Windows "开始**" 中，键入 " **设备和打印机**"。

7.  单击 " **添加打印机**"。

    ![添加打印机](images/g-code-3.png)

8.  选择 **未列出所需的打印机**。

    ![添加设备](images/g-code-4.png)

9.  选择 " **使用手动设置添加本地打印机或网络打印机**"，然后单击 " **下一步**"。

    ![使用手动设置添加本地打印机或网络打印机](images/g-code-5.png)

10. 选择 " **创建新端口** "，为 "端口类型" 选择 " **3d 端口** "，然后单击 " **下一步**"。

    ![创建新端口](images/g-code-6.png)

11. 输入端口名称，然后单击 **"确定"**。

    ![输入端口名称](images/g-code-7.png)

12. 单击 **“从磁盘安装...”**。

    ![有磁盘 .。。](images/g-code-8.png)

13. 从 SDK 浏览到一般3D 打印驱动程序二进制包，并单击 **"确定"**。

14. 单击 **“下一步”** 。

    ![安装打印机驱动程序](images/g-code-9.png)

15. 如果希望 (它将显示在打印机 UI) 中，则可以在此处更改3D 打印机名称，然后单击 " **下一步**"，然后单击 **"确定"** 以允许以管理员身份运行该命令。

    ![键入打印机名称](images/g-code-10.png)

16. 安装完成后，单击 " **完成**"。
