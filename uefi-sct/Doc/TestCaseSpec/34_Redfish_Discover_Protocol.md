# Redfish Discover Protocol Test

## EFI_REDFISH_DISCOVER_PROTOCOL Function Test

**Reference Document:**

*UEFI Specification 2.8*, EFI_REDFISH_DISCOVER_PROTOCOL Section.

*Mantis 1920*, *Mantis 1925*, *Mantis 2172* (UEFI 2.8C).

### GetNetworkInterfaceList() Function

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.1.1.1 | gRedfishDiscoverFunctionTestAssertionGuid001 | **EFI_REDFISH_DISCOVER_PROTOCOL.GetNetworkInterfaceList** – returns valid interface list. | 1. Call **GetNetworkInterfaceList()** with valid parameters. The return status should be **EFI_SUCCESS** and *NumberOfNetworkInterfaces* should be non-zero. |
| 5.34.1.1.2 | gRedfishDiscoverFunctionTestAssertionGuid002 | **EFI_REDFISH_DISCOVER_PROTOCOL.GetNetworkInterfaceList** – interface count is consistent across calls. | 1. Call **GetNetworkInterfaceList()** twice. The *NumberOfNetworkInterfaces* returned should be identical. |

### AcquireRedfishService() Function

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.1.2.1 | gRedfishDiscoverFunctionTestAssertionGuid003 | **EFI_REDFISH_DISCOVER_PROTOCOL.AcquireRedfishService** – synchronous discovery via host interface. | 1. Call **AcquireRedfishService()** with **EFI_REDFISH_DISCOVER_HOST_INTERFACE** flag and a valid token. The return status should be **EFI_SUCCESS** or a supported-infrastructure-dependent result. |

### AbortAcquireRedfishService() Function

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.1.3.1 | gRedfishDiscoverFunctionTestAssertionGuid004 | **EFI_REDFISH_DISCOVER_PROTOCOL.AbortAcquireRedfishService** – basic abort with NULL target. | 1. Call **AbortAcquireRedfishService()**. The return status should be **EFI_SUCCESS** or **EFI_NOT_FOUND** (no pending discovery). |

### ReleaseRedfishService() Function

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.1.4.1 | gRedfishDiscoverFunctionTestAssertionGuid005 | **EFI_REDFISH_DISCOVER_PROTOCOL.ReleaseRedfishService** – release with empty list. | 1. Call **ReleaseRedfishService()** with a valid but empty service list. The return status should be **EFI_SUCCESS**. |


## EFI_REDFISH_DISCOVER_PROTOCOL Conformance Test

**Reference Document:**

*UEFI Specification 2.8*, EFI_REDFISH_DISCOVER_PROTOCOL Section.

*Mantis 1925*, *Mantis 2172* (UEFI 2.8C revised definitions).

### GetNetworkInterfaceList() Conformance

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.2.1.1 | gRedfishDiscoverConformanceTestAssertionGuid001 | **EFI_REDFISH_DISCOVER_PROTOCOL.GetNetworkInterfaceList** – NULL *NumberOfNetworkInterfaces* returns **EFI_INVALID_PARAMETER**. | 1. Call **GetNetworkInterfaceList()** with NULL *NumberOfNetworkInterfaces*. The return status should be **EFI_INVALID_PARAMETER**. |
| 5.34.2.1.2 | gRedfishDiscoverConformanceTestAssertionGuid002 | **EFI_REDFISH_DISCOVER_PROTOCOL.GetNetworkInterfaceList** – NULL *NetworkInterfaces* returns **EFI_INVALID_PARAMETER**. | 1. Call **GetNetworkInterfaceList()** with NULL *NetworkInterfaces*. The return status should be **EFI_INVALID_PARAMETER**. |
| 5.34.2.1.3 | gRedfishDiscoverConformanceTestAssertionGuid006 | **EFI_REDFISH_DISCOVER_PROTOCOL.GetNetworkInterfaceList** – NULL *ImageHandle* returns **EFI_INVALID_PARAMETER** (Mantis 2172). | 1. Call **GetNetworkInterfaceList()** with NULL *ImageHandle*. The return status should be **EFI_INVALID_PARAMETER**. |

### AcquireRedfishService() Conformance

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.2.2.1 | gRedfishDiscoverConformanceTestAssertionGuid003 | **EFI_REDFISH_DISCOVER_PROTOCOL.AcquireRedfishService** – NULL *Token* returns **EFI_INVALID_PARAMETER**. | 1. Call **AcquireRedfishService()** with NULL *Token*. The return status should be **EFI_INVALID_PARAMETER**. |
| 5.34.2.2.2 | gRedfishDiscoverConformanceTestAssertionGuid004 | **EFI_REDFISH_DISCOVER_PROTOCOL.AcquireRedfishService** – *Flags* == 0 returns **EFI_INVALID_PARAMETER**. | 1. Call **AcquireRedfishService()** with *Flags* set to zero. The return status should be **EFI_INVALID_PARAMETER**. |
| 5.34.2.2.3 | gRedfishDiscoverConformanceTestAssertionGuid007 | **EFI_REDFISH_DISCOVER_PROTOCOL.AcquireRedfishService** – **EFI_REDFISH_DISCOVER_VALIDATION** flag alone returns **EFI_INVALID_PARAMETER** (Mantis 2172). | 1. Call **AcquireRedfishService()** with only the **EFI_REDFISH_DISCOVER_VALIDATION** flag set (no base discovery flag). The return status should be **EFI_INVALID_PARAMETER** because VALIDATION is a modifier, not a standalone method. |
| 5.34.2.2.4 | gRedfishDiscoverConformanceTestAssertionGuid008 | **EFI_REDFISH_DISCOVER_PROTOCOL.AcquireRedfishService** – NULL *ImageHandle* returns **EFI_INVALID_PARAMETER** (Mantis 2172). | 1. Call **AcquireRedfishService()** with NULL *ImageHandle*. The return status should be **EFI_INVALID_PARAMETER**. |

### ReleaseRedfishService() Conformance

| Number | GUID | Assertion | Test Description |
|--------|------|-----------|------------------|
| 5.34.2.3.1 | gRedfishDiscoverConformanceTestAssertionGuid005 | **EFI_REDFISH_DISCOVER_PROTOCOL.ReleaseRedfishService** – NULL *List* returns **EFI_INVALID_PARAMETER**. | 1. Call **ReleaseRedfishService()** with NULL *List*. The return status should be **EFI_INVALID_PARAMETER**. |
