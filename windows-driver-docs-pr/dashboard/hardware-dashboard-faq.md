---
title: 硬件仪表板常见问题
description: 本文提供了有关 Windows 硬件开发人员中心仪表板的常见问题解答。
ms.assetid: AA3D1147-7015-4D21-84A6-D127F57DDC97
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adf36c73e4ba615b0bf0982bfec2df38c882eda7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518418"
---
# <a name="hardware-dashboard-faq"></a>硬件仪表板常见问题


本文提供了有关 Windows 硬件开发人员中心仪表板的常见问题解答。

## <a name="span-idhowdoicontacthardwaredevcenterdashboardsupportspanspan-idhowdoicontacthardwaredevcenterdashboardsupportspanspan-idhowdoicontacthardwaredevcenterdashboardsupportspanhow-do-i-contact-hardware-dev-center-dashboard-support"></a><span id="How_do_I_contact_Hardware_Dev_Center_Dashboard_Support_"></span><span id="how_do_i_contact_hardware_dev_center_dashboard_support_"></span><span id="HOW_DO_I_CONTACT_HARDWARE_DEV_CENTER_DASHBOARD_SUPPORT_"></span>如何联系硬件开发人员中心仪表板支持？

如果你在访问仪表板时遇到问题或需要仪表板支持，请在此处开具支持票证： https://developer.microsoft.com/windows/support。  依次选择“联系我们”、“仪表板问题”，然后从下拉列表中选择“硬件提交和签名(所有 OS 版本)”。


## <a name="span-idcaniassociatemultiplecertificateswithadashboardaccountspanspan-idcaniassociatemultiplecertificateswithadashboardaccountspanspan-idcaniassociatemultiplecertificateswithadashboardaccountspancan-i-associate-multiple-certificates-with-a-dashboard-account"></a><span id="Can_I_associate_multiple_certificates_with_a_dashboard_account_"></span><span id="can_i_associate_multiple_certificates_with_a_dashboard_account_"></span><span id="CAN_I_ASSOCIATE_MULTIPLE_CERTIFICATES_WITH_A_DASHBOARD_ACCOUNT_"></span>是否可以将多个证书与一个仪表板帐户相关联？


一个组织可以将多个证书与其仪表板帐户关联在一起。 必须使用这些证书中的任何一个对提交进行签名。

对与组织关联的证书（EV 和标准证书）数量没有限制。

## <a name="span-idwhatagreementsneedtobesignedspanspan-idwhatagreementsneedtobesignedspanspan-idwhatagreementsneedtobesignedspanwhat-agreements-need-to-be-signed"></a><span id="What_agreements_need_to_be_signed_"></span><span id="what_agreements_need_to_be_signed_"></span><span id="WHAT_AGREEMENTS_NEED_TO_BE_SIGNED_"></span>需要签署哪些协议？


在注册过程中，可能会签署以下协议。

> [!NOTE]
> 所有注册都必须签署 Windows 硬件兼容性计划测试协议。 其他所有协议都是可选的，除非你使用其他关联协议中所述的功能或资产。 

-   Windows 硬件兼容性计划测试协议（2.0 版）

-   硬件徽标许可协议（2017 版）

-   UEFI 附录

-   Windows 错误报告 (WER) 协议（1.3 版）

## <a name="span-idhowdoiaddadditionalusersorgrantadditionalrolestousersinmycompanyspanspan-idhowdoiaddadditionalusersorgrantadditionalrolestousersinmycompanyspanspan-idhowdoiaddadditionalusersorgrantadditionalrolestousersinmycompanyspanhow-do-i-add-additional-users-or-grant-additional-roles-to-users-in-my-company"></a><span id="How_do_I_add_additional_users_or_grant_additional_roles_to_users_in_my_company_"></span><span id="how_do_i_add_additional_users_or_grant_additional_roles_to_users_in_my_company_"></span><span id="HOW_DO_I_ADD_ADDITIONAL_USERS_OR_GRANT_ADDITIONAL_ROLES_TO_USERS_IN_MY_COMPANY_"></span>如何添加其他用户或向公司中的用户授予其他角色？


有关详细信息，请参阅[管理用户角色](managing-user-roles.md)。

## <a name="span-idmanagingsubmissionsspanspan-idmanagingsubmissionsspanspan-idmanagingsubmissionsspanmanaging-submissions"></a><span id="Managing_submissions"></span><span id="managing_submissions"></span><span id="MANAGING_SUBMISSIONS"></span>管理提交


### <a name="span-idwhatisthehardwarecertificationsubmissionprocessingtimespanspan-idwhatisthehardwarecertificationsubmissionprocessingtimespanspan-idwhatisthehardwarecertificationsubmissionprocessingtimespanwhat-is-the-hardware-certification-submission-processing-time"></a><span id="What__is_the_hardware_certification_submission_processing_time_"></span><span id="what__is_the_hardware_certification_submission_processing_time_"></span><span id="WHAT__IS_THE_HARDWARE_CERTIFICATION_SUBMISSION_PROCESSING_TIME_"></span>硬件认证提交处理时间为多久？

提交到仪表板的硬件将在五个工作日或更少时间内进行处理，具体取决于提交是否需要手动检查。 如果提交测试失败、没有应用有效筛选器或由于内部业务策略的原因，可能需要手动检查。

### <a name="span-idwhydoiseeadifferenceindownloadsignedfilesspanspan-idwhydoiseeadifferenceindownloadsignedfilesspanspan-idwhydoiseeadifferenceindownloadsignedfilesspanwhy-do-i-see-a-difference-in-download-signed-files"></a><span id="Why_do_I_see_a_difference_in_download_signed_files_"></span><span id="why_do_i_see_a_difference_in_download_signed_files_"></span><span id="WHY_DO_I_SEE_A_DIFFERENCE_IN_DOWNLOAD_SIGNED_FILES_"></span>在下载的已签名文件中，为何存在差异？

为了使 Windows 10 更加安全并且性能不受影响，所有二进制文件现在均要接收嵌入式签名。 这适用于认证的所有提交，而不仅限于 Windows 10 提交。

### <a name="span-idhowtogetasinglecatfileifdriversareuniformforalloperatingsystemsspanspan-idhowtogetasinglecatfileifdriversareuniformforalloperatingsystemsspanspan-idhowtogetasinglecatfileifdriversareuniformforalloperatingsystemsspanhow-to-get-a-single-cat-file-if-drivers-are-uniform-for-all-operating-systems"></a><span id="How_to_get_a_single_cat_file_if_drivers_are_uniform_for_all_operating_systems"></span><span id="how_to_get_a_single_cat_file_if_drivers_are_uniform_for_all_operating_systems"></span><span id="HOW_TO_GET_A_SINGLE_CAT_FILE_IF_DRIVERS_ARE_UNIFORM_FOR_ALL_OPERATING_SYSTEMS"></span>如果驱动程序对所有操作系统都是统一的，如何获取单个 cat 文件？

请在“程序包”选项卡上确保最终的程序包具有单个驱动程序文件夹，并且该驱动程序的属性包含你已测试过的所有操作系统。 有关详细信息，请参阅[演练：如何获取由 Microsoft 签名的适用于多个版本的 Windows 的驱动程序](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)。

### <a name="span-idimunabletoaddnewmarketingnamestotheapprovedsubmissionspanspan-idimunabletoaddnewmarketingnamestotheapprovedsubmissionspanspan-idimunabletoaddnewmarketingnamestotheapprovedsubmissionspanim-unable-to-add-new-marketing-names-to-the-approved-submission"></a><span id="I_m_unable_to_add_new_marketing_names_to_the_approved_submission"></span><span id="i_m_unable_to_add_new_marketing_names_to_the_approved_submission"></span><span id="I_M_UNABLE_TO_ADD_NEW_MARKETING_NAMES_TO_THE_APPROVED_SUBMISSION"></span>无法将新的营销名称添加到已批准的提交

检查已设置的发布日期。 如果发布日期已过，将无法添加新的名称。

### <a name="how-can-i-share-a-link-to-a-windows-certification-verification-report"></a>如何共享 Windows 认证验证报告的链接？
-   可共享 URL 包含三个由斜杠分隔的标识号，如下所示：`https://developer.microsoft.com/dashboard/hardware/driver/DownloadCertificationReport/SellerID/PrivateProductID/SubmissionID`

- URL 中使用的标识号及其位置如下所示：

| Component | 描述 |
| ---       | ---         |
|SellerID   | 合作伙伴帐户的标识号。 可以在帐户管理页上的**帐户设置**下，找到该标识号。 |
|PrivateProductID | 每次创建产品时生成的标识号。 位于产品的驱动程序详细信息页上。 请参阅[仪表板 ID 定义](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)，了解详细信息。 |
|SubmissionID | 指定给每个提交和提交更新的标识号。 位于产品的驱动程序详细信息页上。 请参阅[仪表板 ID 定义](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)，了解详细信息。 |

- 若要创建可共享链接，请将以上示例 URL 中的 **SellerID**、**PrivateProductID** 和 **SubmissionID** 替换为相应的标识号。
- 无需事先获得授权或 Windows 硬件开发人员中心仪表板的访问权限，便可通过此 URL 访问并下载报告。   


## <a name="span-idtroubleshootingsubmissionuploaderrorsspanspan-idtroubleshootingsubmissionuploaderrorsspanspan-idtroubleshootingsubmissionuploaderrorsspantroubleshooting-submission-upload-errors"></a><span id="Troubleshooting_submission_upload_errors"></span><span id="troubleshooting_submission_upload_errors"></span><span id="TROUBLESHOOTING_SUBMISSION_UPLOAD_ERRORS"></span>解决提交上传错误


### <a name="span-idmydriversigningsubmissionfailswiththeerrortherearefilesattherootofthecabinetornoinffilesfoundindriverdirectorydirectoriesxyzspanspan-idmydriversigningsubmissionfailswiththeerrortherearefilesattherootofthecabinetornoinffilesfoundindriverdirectorydirectoriesxyzspanspan-idmydriversigningsubmissionfailswiththeerrortherearefilesattherootofthecabinetornoinffilesfoundindriverdirectorydirectoriesxyzspanmy-driver-signing-submission-fails-with-the-error-there-are-files-at-the-root-of-the-cabinet-or-no-inf-files-found-in-driver-directorydirectories-xyz"></a><span id="My_driver_signing_submission_fails_with_the_error__There_are_files_at_the_root_of_the_cabinet__or___No_.inf_files_found_in_driver_directory_directories__XYZ_"></span><span id="my_driver_signing_submission_fails_with_the_error__there_are_files_at_the_root_of_the_cabinet__or___no_.inf_files_found_in_driver_directory_directories__xyz_"></span><span id="MY_DRIVER_SIGNING_SUBMISSION_FAILS_WITH_THE_ERROR__THERE_ARE_FILES_AT_THE_ROOT_OF_THE_CABINET__OR___NO_.INF_FILES_FOUND_IN_DRIVER_DIRECTORY_DIRECTORIES__XYZ_"></span>驱动程序签名提交失败，并显示错误“在 Cabinet 根处有文件”或者“在以下驱动程序目录中找到了 \#No 个 .inf 文件：XYZ”

失败是由 .cab 文件的结构错误导致。 .cab 结构是使用 .cab 文件的根文件夹中的驱动程序文件创建，而非将它们置于子文件夹中。 有关如何为驱动程序签名提交创建正确的 .cab 文件的说明，请参阅[对内核驱动程序进行证明签名以便公开发布](attestation-signing-a-kernel-driver-for-public-release.md)。

### <a name="span-iditlookslikeyourpackageiscorruptormissingimportantinformationensureyouareusingthelatestversionofthekitregenerateyourpackageandtryagainifyoucontinuetoexperiencetheissuecontactsupportspanspan-iditlookslikeyourpackageiscorruptormissingimportantinformationensureyouareusingthelatestversionofthekitregenerateyourpackageandtryagainifyoucontinuetoexperiencetheissuecontactsupportspanspan-iditlookslikeyourpackageiscorruptormissingimportantinformationensureyouareusingthelatestversionofthekitregenerateyourpackageandtryagainifyoucontinuetoexperiencetheissuecontactsupportspanit-looks-like-your-package-is-corrupt-or-missing-important-information-ensure-you-are-using-the-latest-version-of-the-kit-regenerate-your-package-and-try-again-if-you-continue-to-experience-the-issue-contact-support"></a><span id="_It_looks_like_your_package_is_corrupt_or_missing_important_information._Ensure_you_are_using_the_latest_version_of_the_kit__regenerate_your_package__and_try_again._If_you_continue_to_experience_the_issue__contact_Support._"></span><span id="_it_looks_like_your_package_is_corrupt_or_missing_important_information._ensure_you_are_using_the_latest_version_of_the_kit__regenerate_your_package__and_try_again._if_you_continue_to_experience_the_issue__contact_support._"></span><span id="_IT_LOOKS_LIKE_YOUR_PACKAGE_IS_CORRUPT_OR_MISSING_IMPORTANT_INFORMATION._ENSURE_YOU_ARE_USING_THE_LATEST_VERSION_OF_THE_KIT__REGENERATE_YOUR_PACKAGE__AND_TRY_AGAIN._IF_YOU_CONTINUE_TO_EXPERIENCE_THE_ISSUE__CONTACT_SUPPORT._"></span>“似乎程序包已损坏或丢失了重要信息。 请确保使用最新版本的工具包，重新生成程序包，然后再试一次。 如果仍遇到问题，请联系支持人员。”

如果仍遇到程序包提交问题，请与仪表板标头中所列的支持人员联系。

### <a name="span-idfileisusingzip644gbfilesizespanspan-idfileisusingzip644gbfilesizespanspan-idfileisusingzip644gbfilesizespanfile-is-using-zip644gbfile-size"></a><span id="File_is_using_Zip64_4gb_file_Size_"></span><span id="file_is_using_zip64_4gb_file_size_"></span><span id="FILE_IS_USING_ZIP64_4GB_FILE_SIZE_"></span>“文件使用的是 Zip64 (文件大小超过 4GB)”

当上传的存档文件类型为 .zip64 而不是 .zip 时，会导致发生该错误。 这由文件大小较大导致。 若要修复该错误，请按照以下步骤操作重新打包提交。

1.  将当前的 .hckx/hlkx 文件重命名为 .zip。
2.  解压缩到某个文件夹。
3.  打开该文件夹。
4.  选择所有项目，然后右键单击并选择“发送到压缩 zip 文件夹”。
5.  将新的 .zip 文件夹重命名为 .hckx/.hlkx。
6.  上载新的 .hckx/.hlkx 文件。

### <a name="span-idtheduapackageerrorshowsfailedtoopenpackagewiththeerrornotcompatiblewithaversion3200withthisinstancepackagemanagerspanspan-idtheduapackageerrorshowsfailedtoopenpackagewiththeerrornotcompatiblewithaversion3200withthisinstancepackagemanagerspanspan-idtheduapackageerrorshowsfailedtoopenpackagewiththeerrornotcompatiblewithaversion3200withthisinstancepackagemanagerspanthe-dua-package-error-shows-failed-to-open-package-with-the-error-not-compatible-with-a-version-3200-with-this-instance-package-manager"></a><span id="The_DUA_package_error_shows__Failed_to_open_package__with_the_error__Not_compatible_with_a_version__3.2.0.0__with_this_instance_package_manager_"></span><span id="the_dua_package_error_shows__failed_to_open_package__with_the_error__not_compatible_with_a_version__3.2.0.0__with_this_instance_package_manager_"></span><span id="THE_DUA_PACKAGE_ERROR_SHOWS__FAILED_TO_OPEN_PACKAGE__WITH_THE_ERROR__NOT_COMPATIBLE_WITH_A_VERSION__3.2.0.0__WITH_THIS_INSTANCE_PACKAGE_MANAGER_"></span>DUA 程序包错误显示“无法打开程序包”以及错误“与包含此实例程序包管理器的版本 (3.2.0.0) 不兼容”

-   使用 [HLK Studio](https://msdn.microsoft.com/library/windows/hardware/dn939927) 来打开下载的 DUA shell 程序包，并创建 DUA 提交。

 

 

