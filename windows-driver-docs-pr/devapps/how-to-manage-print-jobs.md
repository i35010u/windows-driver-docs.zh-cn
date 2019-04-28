---
title: 如何管理 UWP 设备应用中的打印作业
description: 在 Windows 8.1，UWP 应用的打印机的设备应用程序可以管理打印作业。
ms.assetid: 30E247DB-E5B0-4CD5-89F5-4227EE20A564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea61ec736cb596a7c1b8d36dd379fc04923cf8aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330696"
---
# <a name="how-to-manage-print-jobs-in-a-uwp-device-app"></a>如何管理 UWP 设备应用中的打印作业


在 Windows 8.1，UWP 应用的打印机的设备应用程序可以管理打印作业。 本主题使用C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例，用于演示如何创建一个视图的打印作业、 监视这些作业，并如有必要，取消的作业。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例演示如何使用打印机维护**DeviceMaintenance.xaml.cs**中的文件**DeviceAppForPrinters2**项目。 若要使用 Bidi，该示例使用的打印机扩展库中**PrinterExtensionLibrary**项目。 打印机扩展库提供了方便地访问 v4 打印驱动程序的打印机扩展插件接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例。 此示例也会出现在 JavaScript 和C++。 请注意，由于C++可以直接访问 COMC++示例的版本不包括代码库项目。 下载示例，请参阅最新版本的代码。

 

## <a name="span-idmanagingprintjobsspanspan-idmanagingprintjobsspanspan-idmanagingprintjobsspanmanaging-print-jobs"></a><span id="Managing_print_jobs"></span><span id="managing_print_jobs"></span><span id="MANAGING_PRINT_JOBS"></span>管理打印作业


Windows 8.1 引入了新的 v4 打印机驱动程序可用于管理打印作业中的打印机扩展插件接口：[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)， [ **IPrinterQueueView**](https://msdn.microsoft.com/library/windows/hardware/dn265392)， [ **IPrinterQueueViewEvent**](https://msdn.microsoft.com/library/windows/hardware/dn265393)， [ **IPrintJob**](https://msdn.microsoft.com/library/windows/hardware/dn265396)，并[ **IPrintJobCollection**](https://msdn.microsoft.com/library/windows/hardware/dn265397)。 这些接口，让可以监视和取消打印作业。 有关详细信息，请参阅[打印作业管理 （v4 打印机驱动程序）](https://msdn.microsoft.com/library/windows/hardware/dn265419)。

**提示**   C#和 JavaScript 应用程序不能直接使用 COM Api。 如果您要编写C#或 JavaScript UWP 设备应用，使用打印机扩展库来访问这些接口 （如本主题中所示）。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保使用 v4 打印驱动程序安装您的打印机。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
3.  将你的应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
4.  创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
5.  构建您的应用程序的主页上的 UI。 可以从开始，它们将显示的全屏启动所有 UWP 设备应用程序。 使用入门体验突出显示你的产品或匹配特定品牌的方式和你的设备的功能中的服务。 没有任何特殊限制可以使用 UI 控件的类型。 若要开始使用的设计的全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6.  如果您正在编写您编写的应用程序与C#或 JavaScript 中，添加**PrinterExtensionLibrary**到 UWP 设备应用程序解决方案的项目。 您可以找到此项目中的[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例。
    **请注意**  由于C++可以直接访问 COMC++应用程序不需要单独的库以使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep1findprinterspanspan-idstep1findprinterspanspan-idstep1findprinterspanstep-1-find-printer"></a><span id="Step_1__Find_printer"></span><span id="step_1__find_printer"></span><span id="STEP_1__FIND_PRINTER"></span>步骤 1：查找打印机


您的应用程序可以管理打印作业之前，它首先必须找到拥有打印作业的打印机。 若要执行此操作，[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例包含一个名为的方便类`PrinterEnumeration`(在**PrinterEnumeration.cs**文件)。 此类查找与您的应用程序通过设备元数据相关联的所有打印机并返回一系列`PrinterInfo`对象，包含为每个打印机的设备 Id 和名称。

此示例演示`EnumeratePrinters_Click`中的方法**PrintJobManagement.xaml.cs**文件。 它显示如何使用示例`PrinterEnumeration`类，以获取一组相关联的打印机。

```CSharp
private async void EnumeratePrinters_Click(object sender, RoutedEventArgs e)
{
    try
    {
        rootPage.NotifyUser("Enumerating printers. Please wait", NotifyType.StatusMessage);

        // Retrieve the running app's package family name, and enumerate associated printers.
        string currentPackageFamilyName = Windows.ApplicationModel.Package.Current.Id.FamilyName;

        // Enumerate associated printers.
        PrinterEnumeration pe = new PrinterEnumeration(currentPackageFamilyName);
        List<PrinterInfo> associatedPrinters = await pe.EnumeratePrintersAsync();

        // Update the data binding source on the combo box that displays the list of printers.
        PrinterComboBox.ItemsSource = associatedPrinters;
        if (associatedPrinters.Count > 0)
        {
            PrinterComboBox.SelectedIndex = 0;
            rootPage.NotifyUser(associatedPrinters.Count + " printers enumerated", NotifyType.StatusMessage);
        }
        else
        {
            rootPage.NotifyUser(DisplayStrings.NoPrintersEnumerated, NotifyType.ErrorMessage);
        }
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

**提示**  有关详细信息`PrinterEnumeration`并`PrinterInfo`类，请参见**PrinterEnumeration.cs**文件。

 

## <a name="span-idstep2getprinterqueuespanspan-idstep2getprinterqueuespanspan-idstep2getprinterqueuespanstep-2-get-printer-queue"></a><span id="Step_2__Get_printer_queue"></span><span id="step_2__get_printer_queue"></span><span id="STEP_2__GET_PRINTER_QUEUE"></span>步骤 2：获取打印机队列


一旦具有你想要管理，创建的打印作业的打印机*视图*打印作业，使用基于对象的`IPrinterQueueView`接口 (在中定义**PrinterExtensionTypes.cs**的文件**PrinterExtensionLibrary**项目)。 在中[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例中，此对象名为`currentPrinterQueueView`并重新创建打印机选择更改每个时间。

在中`Printer_SelectionChanged`方法，该示例首先使用`PrinterInfo`对象来创建一个名为打印机扩展上下文对象`context`。 然后，它使用`GetPrinterQueueView`方法`context`若要创建`currentPrinterQueueView`对象。 最后，添加一个事件处理程序来处理`currentPrinterQueueView`的`OnChanged`事件。

此示例演示`Printer_SelectionChanged`中的方法**PrintJobManagement.xaml.cs**文件。 它演示如何创建基于的打印机队列视图对象`IPrinterQueueView`。

```CSharp
private void Printer_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    try
    {
        // Remove the current printer queue view (if any) before displaying the new view.
        if (currentPrinterQueueView != null)
        {
            currentPrinterQueueView.OnChanged -= OnPrinterQueueViewChanged;
            currentPrinterQueueView = null;
        }

        // Retrieve a COM IPrinterExtensionContext object, using the static WinRT factory.
        // Then instantiate one "PrinterExtensionContext" object that allows operations on the COM object.
        PrinterInfo queue = (PrinterInfo)PrinterComboBox.SelectedItem;
        Object comComtext = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(queue.DeviceId);
        PrinterExtensionContext context = new PrinterExtensionContext(comComtext);

        // Display the printer queue view.
        const int FirstPrintJobEnumerated = 0;
        const int LastPrintJobEnumerated = 10;

        currentPrinterQueueView = context.Queue.GetPrinterQueueView(FirstPrintJobEnumerated, LastPrintJobEnumerated);
        currentPrinterQueueView.OnChanged += OnPrinterQueueViewChanged;
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

此外，每当对打印作业的视图的更改时，事件处理程序会调用`OnPrinterQueueViewChanged`方法。 此方法负责重新绑定`PrintJobListBox`与 IEnumerable 集合的`IPrintJob`对象。 集合传递给该方法通过`PrinterQueueViewEventArgs`对象中定义**PrinterExtensionTypes.cs**文件。

此示例演示`OnPrinterQueueViewChanged`中的方法**PrintJobManagement.xaml.cs**文件。

```CSharp
private async void OnPrinterQueueViewChanged(object sender, PrinterQueueViewEventArgs e)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        // Update the data binding on the ListBox that displays print jobs.
        PrintJobListBox.ItemsSource = e.Collection;
        if (PrintJobListBox.Items.Count > 0)
        {
            // If there are print jobs in the current view, mark the first job as selected.
            PrintJobListBox.SelectedIndex = 0;
        }
    });
}
```

## <a name="span-idstep3displayprintjobstatusspanspan-idstep3displayprintjobstatusspanspan-idstep3displayprintjobstatusspanstep-3-display-print-job-status"></a><span id="Step_3__Display_print_job_status"></span><span id="step_3__display_print_job_status"></span><span id="STEP_3__DISPLAY_PRINT_JOB_STATUS"></span>步骤 3：显示打印作业状态


因为`PrintJobListBox`绑定到的集合`IPrintJob`对象，显示作业的状态是非常简单。 所选的打印作业被强制转换为`IPrintJob`对象，然后该对象的属性用于填充`PrintJobDetails`文本框中。

在中[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例，显示选择了不同的打印作业每次打印作业状态。 此更新是由负责`PrintJob_SelectionChanged`方法。

此示例演示`PrintJob_SelectionChanged`中的方法**PrintJobManagement.xaml.cs**文件。 它演示了如何显示根据的打印作业的状态`IPrintJob`对象。

```CSharp
private void PrintJob_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    try
    {
        // Display details of the selected print job.
        IPrintJob job = (IPrintJob)PrintJobListBox.SelectedItem;
        if (job != null)
        {
            PrintJobDetails.Text =
                "Details of print job: " + job.Name + "\r\n" +
                "Pages printed: " + job.PrintedPages + "/" + job.TotalPages + "\r\n" +
                "Submission time: " + job.SubmissionTime + "\r\n" +
                "Job status: " + DisplayablePrintJobStatus.ToString(job.Status);
        }
        else
        {
            PrintJobDetails.Text = "Please select a print job";
        }
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

若要帮助将显示在打印作业状态说明，`PrintJob_SelectionChanged`方法使用一个名为的静态词典`printJobStatusDisplayNames`，以帮助将显示在采用用户友好的文本格式的作业状态说明。

此示例演示`DisplayablePrintJobStatus`类中**PrintJobManagement.xaml.cs**文件。 此类包含使用的静态成员`PrintJob_SelectionChanged`。

```CSharp
internal class DisplayablePrintJobStatus
{
    /// <summary>
    /// Converts the PrintJobStatus bit fields to a display string.
    /// </summary>
    internal static string ToString(PrintJobStatus printJobStatus)
    {
        StringBuilder statusString = new StringBuilder();

        // Iterate through each of the PrintJobStatus bits that are set and convert it to a display string.
        foreach (var printJobStatusDisplayName in printJobStatusDisplayNames)
        {
            if ((printJobStatusDisplayName.Key & printJobStatus) != 0)
            {
                statusString.Append(printJobStatusDisplayName.Value);
            }
        }

        int stringlen = statusString.Length;
        if (stringlen > 0)
        {
            // Trim the trailing comma from the string.
            return statusString.ToString(0, stringlen - 1);
        }
        else
        {
            // If no print job status field was set, display "Not available".
            return "Not available";
        }
    }

    /// <summary>
    /// Static constructor that initializes the display name for the PrintJobStatus field.
    /// </summary>
    static DisplayablePrintJobStatus()
    {
        printJobStatusDisplayNames = new Dictionary<PrintJobStatus, string>();

        printJobStatusDisplayNames.Add(PrintJobStatus.Paused, "Paused,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Error, "Error,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Deleting, "Deleting,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Spooling, "Spooling,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Printing, "Printing,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Offline, "Offline,");
        printJobStatusDisplayNames.Add(PrintJobStatus.PaperOut, "Out of paper,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Printed, "Printed,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Deleted, "Deleted,");
        printJobStatusDisplayNames.Add(PrintJobStatus.BlockedDeviceQueue, "Blocked device queue,");
        printJobStatusDisplayNames.Add(PrintJobStatus.UserIntervention, "User intervention required,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Restarted, "Restarted,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Complete, "Complete,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Retained, "Retained,");
    }
    
    /// <summary>
    /// Private constructor to prevent default instantiation.
    /// </summary>
    private DisplayablePrintJobStatus() { }

    /// <summary>
    /// Contains the mapping between PrintJobStatus fields and display strings.
    /// </summary>
    private static Dictionary<PrintJobStatus, string> printJobStatusDisplayNames;
}
```

## <a name="span-idstep4cancelprintjobspanspan-idstep4cancelprintjobspanspan-idstep4cancelprintjobspanstep-4-cancel-print-job"></a><span id="Step_4__Cancel_print_job"></span><span id="step_4__cancel_print_job"></span><span id="STEP_4__CANCEL_PRINT_JOB"></span>步骤 4：取消打印作业


类似于显示打印作业状态，正在取消打印作业是非常简单，有时`IPrintJob`对象。 `IPrintJob`类提供了`RequestCancel`启动相应的打印作业的取消操作的方法。 在此示例中对此进行了演示`CancelPrintJob_Click`方法。

此示例演示`CancelPrintJob_Click`中的方法**PrintJobManagement.xaml.cs**文件。

```CSharp
private void CancelPrintJob_Click(object sender, RoutedEventArgs e)
{
    try
    {
        IPrintJob job = (IPrintJob)PrintJobListBox.SelectedItem;
        job.RequestCancel();
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

## <a name="span-idtestingspanspan-idtestingspantesting"></a><span id="testing"></span><span id="TESTING"></span>测试


你可以测试 UWP 设备应用之前，它必须链接到您的打印机使用的设备元数据。

-   需要打印机的位置，若要向其中添加设备应用信息的设备元数据包的副本。 如果没有设备元数据，您可以使用生成它**设备元数据创建向导**主题中所述[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    **请注意**  若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)之前完成本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

     

以下步骤生成您的应用程序并安装设备元数据。

1.  启用测试签名。
    1.  启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**
    2.  从**工具**菜单中，选择**启用测试签名**。

2.  重新启动计算机
3.  通过打开解决方案 (.sln) 文件生成解决方案。 按 F7，或转至**生成-&gt;生成解决方案**从顶部菜单中加载示例之后。

4.  断开连接并卸载打印机。 此步骤是必需的以便 Windows 将在下一次检测到设备读取更新的设备元数据。
5.  编辑并保存设备元数据。 要链接到你的设备的设备应用，必须将设备应用与你的设备进行关联。
    **请注意**  如果尚未创建设备元数据，请参阅[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

     

    1.  如果**设备元数据创建向导**未打开，启动从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，也可由双击**DeviceMetadataWizard.exe**。
    2.  单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
    3.  在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
    4.  上**指定 UWP 设备应用信息**页上，输入中的 Microsoft Store 应用信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。
    5.  如果您的应用程序注册的打印机通知，填写**通知处理程序**框。 在中**事件 ID**，输入打印事件处理程序的名称。 在中**事件资产**，输入该代码所在的位置的文件的名称。

    6.  完成后，单击**下一步**直至到达**完成**页。
    7.  上**查看设备元数据包**页面上，确保所有设置都正确，然后选择**复制到本地计算机上的元数据存储设备元数据包**复选框。 然后单击**保存**。

6.  重新连接您的打印机，以便在设备连接时，该 Windows 读取更新的设备元数据。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[作业管理 （v4 打印机驱动程序）](https://msdn.microsoft.com/library/windows/hardware/dn265419)

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






