---
title: 如何在 UWP 设备应用中管理打印作业
description: 在 Windows 8.1 中，用于打印机的 UWP 设备应用可以管理打印作业。
ms.assetid: 30E247DB-E5B0-4CD5-89F5-4227EE20A564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d319ab0e926f270f08084aa9b2e4ef3b7e9aff6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829907"
---
# <a name="how-to-manage-print-jobs-in-a-uwp-device-app"></a>如何在 UWP 设备应用中管理打印作业


在 Windows 8.1 中，用于打印机的 UWP 设备应用可以管理打印作业。 本主题使用C# [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例的版本来演示如何创建打印作业的视图、监视这些作业，并在必要时取消作业。 若要详细了解 UWP 设备应用的详细信息，请参阅了解[uwp 设备应用](meet-uwp-device-apps.md)。

C# [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例的版本演示了在**DeviceAppForPrinters2**项目中通过**DeviceMaintenance.xaml.cs**文件进行的打印机维护。 若要使用双向，示例将在**PrinterExtensionLibrary**项目中使用打印机扩展库。 打印机扩展库提供了一种便捷的方式来访问 v4 打印驱动程序的打印机扩展接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C# [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例的版本。 此示例在 JavaScript 和C++中也可用。 请注意， C++由于可以直接访问 COM， C++因此该示例的版本不包括代码库项目。 下载示例以查看最新版本的代码。

 

## <a name="span-idmanaging_print_jobsspanspan-idmanaging_print_jobsspanspan-idmanaging_print_jobsspanmanaging-print-jobs"></a><span id="Managing_print_jobs"></span><span id="managing_print_jobs"></span><span id="MANAGING_PRINT_JOBS"></span>管理打印作业


Windows 8.1 在 v4 打印机驱动程序中引入了新的打印机扩展接口，可用于管理打印作业： [**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)、 [**IPrinterQueueView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)、 [**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)、 [**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)和[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)。 利用这些接口，可以监视和取消打印作业。 有关详细信息，请参阅[打印作业管理（V4 打印机驱动程序）](https://docs.microsoft.com/windows-hardware/drivers/print/job-management)。

**Tip**  C#和 JavaScript 应用无法直接与 COM api 一起使用。 如果要编写C#或 JavaScript UWP 设备应用，请使用打印机扩展库来访问这些接口（如本主题中所述）。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保您的打印机是使用 v4 打印驱动程序安装的。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  设置开发 PC。 有关下载工具和创建开发人员帐户的信息[，请参阅入门。](getting-started.md)
3.  将应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)了解相关信息。
4.  为打印机创建将其与应用程序关联的设备元数据。 有关详细信息，请参阅[创建设备元数据](step-2--create-device-metadata.md)。
5.  构建应用程序主页的 UI。 所有 UWP 设备应用都可以从 "开始" 启动，它们将全屏显示。 使用 "开始体验" 以与设备的特定品牌和功能匹配的方式突出显示你的产品或服务。 它可以使用的 UI 控件类型没有任何特殊限制。 若要开始设计全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6.  如果你正在编写你的C#应用程序或 JavaScript，请将**PrinterExtensionLibrary**项目添加到 UWP 设备应用解决方案。 可以在[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例中找到此项目。
    **请注意**  C++因为可以直接访问 com C++ ，所以应用不需要单独的库即可使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep_1__find_printerspanspan-idstep_1__find_printerspanspan-idstep_1__find_printerspanstep-1-find-printer"></a><span id="Step_1__Find_printer"></span><span id="step_1__find_printer"></span><span id="STEP_1__FIND_PRINTER"></span>步骤1：查找打印机


在你的应用程序可以管理打印作业之前，它必须首先查找包含打印作业的打印机。 要执行此操作，[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例包含一个名为 `PrinterEnumeration` 的便利类（在**PrinterEnumeration.cs**文件中）。 此类通过设备元数据查找与应用程序关联的所有打印机，并返回 `PrinterInfo` 对象的列表，其中包含每个打印机的名称和设备 Id。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `EnumeratePrinters_Click` 方法。 其中显示了该示例如何使用 `PrinterEnumeration` 类获取关联打印机的列表。

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

**提示**  有关 `PrinterEnumeration` 和 `PrinterInfo` 类的详细信息，请参阅**PrinterEnumeration.cs**文件。

 

## <a name="span-idstep_2__get_printer_queuespanspan-idstep_2__get_printer_queuespanspan-idstep_2__get_printer_queuespanstep-2-get-printer-queue"></a><span id="Step_2__Get_printer_queue"></span><span id="step_2__get_printer_queue"></span><span id="STEP_2__GET_PRINTER_QUEUE"></span>步骤2：获取打印机队列


确定包含要管理的打印作业的打印机后，创建打印作业的*视图*，其中包含基于 `IPrinterQueueView` 接口的对象（在 PrinterExtensionLibrary 的**PrinterExtensionTypes.cs**文件中定义）。项目）。 在[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例中，此对象名为 `currentPrinterQueueView`，并在每次打印机选择更改时重新创建。

在 `Printer_SelectionChanged` 方法中，示例首先使用 `PrinterInfo` 对象创建名为 `context`的打印机扩展上下文对象。 然后，它使用 `context` 上的 `GetPrinterQueueView` 方法来创建 `currentPrinterQueueView` 对象。 最后，添加一个事件处理程序来处理 `currentPrinterQueueView`的 `OnChanged` 事件。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `Printer_SelectionChanged` 方法。 它演示如何基于 `IPrinterQueueView`创建打印机队列视图对象。

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

此外，每当打印作业的视图发生更改时，事件处理程序都会调用 `OnPrinterQueueViewChanged` 方法。 此方法负责使用 `IPrintJob` 对象的 IEnumerable 集合重新绑定 `PrintJobListBox`。 集合通过在**PrinterExtensionTypes.cs**文件中定义的 `PrinterQueueViewEventArgs` 对象传递到方法。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `OnPrinterQueueViewChanged` 方法。

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

## <a name="span-idstep_3__display_print_job_statusspanspan-idstep_3__display_print_job_statusspanspan-idstep_3__display_print_job_statusspanstep-3-display-print-job-status"></a><span id="Step_3__Display_print_job_status"></span><span id="step_3__display_print_job_status"></span><span id="STEP_3__DISPLAY_PRINT_JOB_STATUS"></span>步骤3：显示打印作业状态


由于 `PrintJobListBox` 绑定到 `IPrintJob` 对象的集合，因此显示作业的状态非常简单。 选定的打印作业将强制转换为 `IPrintJob` 对象，然后将使用该对象的属性来填充 `PrintJobDetails` 文本框。

在[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例中，每次选择不同的打印作业时，都会显示打印作业状态。 此更新由 `PrintJob_SelectionChanged` 方法执行。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `PrintJob_SelectionChanged` 方法。 它演示如何根据 `IPrintJob` 对象显示打印作业的状态。

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

为了帮助显示打印作业状态说明，`PrintJob_SelectionChanged` 方法使用名为 `printJobStatusDisplayNames`的静态字典，以帮助显示用户友好文本格式的作业状态说明。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `DisplayablePrintJobStatus` 类。 此类包含 `PrintJob_SelectionChanged`使用的静态成员。

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

## <a name="span-idstep_4__cancel_print_jobspanspan-idstep_4__cancel_print_jobspanspan-idstep_4__cancel_print_jobspanstep-4-cancel-print-job"></a><span id="Step_4__Cancel_print_job"></span><span id="step_4__cancel_print_job"></span><span id="STEP_4__CANCEL_PRINT_JOB"></span>步骤4：取消打印作业


类似于显示打印作业状态，当你有 `IPrintJob` 对象时，取消打印作业非常简单。 `IPrintJob` 类提供 `RequestCancel` 方法来启动对相应打印作业的取消。 示例的 `CancelPrintJob_Click` 方法演示了这一点。

此示例显示了**PrintJobManagement.xaml.cs**文件中的 `CancelPrintJob_Click` 方法。

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


在可以测试 UWP 设备应用之前，必须使用设备元数据将其链接到您的打印机。

-   你需要打印机的设备元数据包的副本，以便向其添加设备应用信息。 如果没有设备元数据，可以使用**设备元数据创作向导**生成它，如主题为[UWP 设备应用创建设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)中所述。

    **请注意**  要使用**设备元数据创作向导**，则必须在完成本主题中的步骤之前，安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或[独立 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

     

以下步骤生成应用并安装设备元数据。

1.  启用测试签名。
    1.  双击**DeviceMetadataWizard** ，从 *% ProgramFiles （x86）%* \\Windows 工具包\\8.1\\Bin\\X86 启动**设备元数据创作向导**
    2.  从 "**工具**" 菜单中，选择 "**启用测试签名**"。

2.  重新启动计算机
3.  通过打开解决方案（.sln）文件来生成解决方案。 加载示例后，按 F7 或从顶部菜单中转到 "**生成-&gt;生成解决方案**"。

4.  断开连接并卸载打印机。 此步骤是必需的，以便 Windows 将在下一次检测到设备时读取更新的设备元数据。
5.  编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备。
    **请注意**  如果尚未创建设备元数据，请参阅为[UWP 设备应用创建设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

     

    1.  如果尚未打开**设备元数据创作向导**，请通过双击**DeviceMetadataWizard**，从 *% ProgramFiles （X86）%* \\Windows 工具包\\8.1\\bin\\x86 启动它。
    2.  单击 "**编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
    3.  在 "**打开**" 对话框中，找到与 UWP 设备应用关联的设备元数据包。 （它具有**devicemetadata 的**文件扩展名。）
    4.  在 "**指定 uwp 设备应用信息**" 页上，在 " **UWP 设备应用**" 框中输入 Microsoft Store 应用信息。 单击 "**导入 UWP 应用程序清单文件**" 以自动输入**包名称**、**发布者名称**和**UWP 应用 ID**。
    5.  如果你的应用正在注册打印机通知，请填写**通知处理程序**框。 在 "**事件 ID**" 中，输入打印事件处理程序的名称。 在 "**事件资产**" 中，输入代码所在的文件的名称。

    6.  完成后，单击 "**下一步**"，直到到达 "**完成**" 页。
    7.  在 "**查看设备元数据包**" 页上，确保所有设置均正确，并选中 "将**设备元数据包复制到本地计算机上的元数据存储区**" 复选框。 然后单击 "**保存**"。

6.  重新连接打印机，以便 Windows 在连接设备时读取更新的设备元数据。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[作业管理（v4 打印机驱动程序）](https://docs.microsoft.com/windows-hardware/drivers/print/job-management)

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用（分步指南）](step-1--create-a-uwp-device-app.md)

[为 UWP 设备应用创建设备元数据（循序渐进指南）](step-2--create-device-metadata.md)

 

 






