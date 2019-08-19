---
title: Когда следует развертывать контейнеры Windows на виртуальных машинах Azure (облачная среда IaaS)
description: Модернизировать существующих приложений .NET с помощью Azure Cloud and Windows Containers | Когда следует развертывать контейнеры Windows на виртуальных машинах Azure (облако IaaS)
ms.date: 04/28/2018
ms.openlocfilehash: e9a2903662306b607977a7751018e24161ab80ab
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577907"
---
# <a name="when-to-deploy-windows-containers-to-azure-vms-iaas-cloud"></a><span data-ttu-id="d8971-103">Когда следует развертывать контейнеры Windows на виртуальных машинах Azure (облачная среда IaaS)</span><span class="sxs-lookup"><span data-stu-id="d8971-103">When to deploy Windows Containers to Azure VMs (IaaS cloud)</span></span>

<span data-ttu-id="d8971-104">Если ваша организация использует виртуальные машины Azure, даже если вы используете контейнеры Windows, вы по-прежнему работаете с IaaS.</span><span class="sxs-lookup"><span data-stu-id="d8971-104">If your organization is using Azure VMs, even if you are also using Windows Containers, you are still dealing with IaaS.</span></span> <span data-ttu-id="d8971-105">Это означает, что при развертывании на нескольких виртуальных машинах в инфраструктуре с балансировкой нагрузки необходимо выполнять операции с инфраструктурой, исправления операционной системы виртуальной машины и сложность инфраструктуры для масштабируемых приложений.</span><span class="sxs-lookup"><span data-stu-id="d8971-105">That means that dealing with infrastructure operations, VM OS patches, and infrastructure complexity for highly scalable applications when you need to deploy to multiple VMs in a load balanced infrastructure.</span></span> <span data-ttu-id="d8971-106">Ниже приведены основные сценарии использования контейнеров Windows на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="d8971-106">The main scenarios for using Windows Containers in an Azure VM are:</span></span>

- <span data-ttu-id="d8971-107">**Среда разработки и тестирования**: Виртуальная машина в облаке идеально подходит для разработки и тестирования в облаке.</span><span class="sxs-lookup"><span data-stu-id="d8971-107">**Dev/test environment**: A VM in the cloud is perfect for development and testing in the cloud.</span></span> <span data-ttu-id="d8971-108">Вы можете быстро создать или прерывать среду в зависимости от ваших потребностей.</span><span class="sxs-lookup"><span data-stu-id="d8971-108">You can rapidly create or stop the environment depending on your needs.</span></span>

- <span data-ttu-id="d8971-109">**Малые и средние требования**к масштабируемости: В сценариях, где вам может потребоваться всего несколько виртуальных машин для рабочей среды, управление небольшим количеством виртуальных машин может быть доступно, пока вы не сможете перейти к более сложным средам PaaS, таким как оркестрации.</span><span class="sxs-lookup"><span data-stu-id="d8971-109">**Small and medium scalability needs**: In scenarios where you might need just a couple of VMs for your production environment, managing a small number of VMs might be affordable until you can move to more advanced PaaS environments, like orchestrators.</span></span>

- <span data-ttu-id="d8971-110">**Рабочая среда с существующими инструментами развертывания**: Вы можете переместиться из локальной среды, в которой были вложены средства для создания сложных развертываний на виртуальных машинах или серверах без операционной системы (например, Puppet или аналогичные средства).</span><span class="sxs-lookup"><span data-stu-id="d8971-110">**Production environment with existing deployment tools**: You might be moving from an on-premises environment in which you have invested in tools to make complex deployments to VMs or bare-metal servers (like Puppet or similar tools).</span></span> <span data-ttu-id="d8971-111">Чтобы перейти в облако с минимальными изменениями в процедурах развертывания рабочей среды, вы можете продолжать использовать эти средства для развертывания на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="d8971-111">To move to the cloud with minimal changes to production environment deployment procedures, you might continue to use those tools to deploy to Azure VMs.</span></span> <span data-ttu-id="d8971-112">Однако для улучшения процесса развертывания в качестве единицы развертывания необходимо использовать контейнеры Windows.</span><span class="sxs-lookup"><span data-stu-id="d8971-112">However, you'll want to use Windows Containers as the unit of deployment to improve the deployment experience.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="d8971-113">[Назад](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
>[Вперед](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)</span><span class="sxs-lookup"><span data-stu-id="d8971-113">[Previous](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
[Next](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)</span></span>