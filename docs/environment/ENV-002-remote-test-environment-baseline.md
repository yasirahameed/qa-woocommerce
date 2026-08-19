# ENV-002 — Remote WooCommerce Test Environment Baseline

## 1. Purpose

This document establishes the initial baseline of the remote WooCommerce test environment before Sprint 1 configuration and test execution.

The baseline is intended to provide traceability for subsequent environment changes and to distinguish pre-existing conditions from conditions introduced during test preparation or execution.

## 2. Environment Identification

| Attribute           | Value                        |
| ------------------- | ---------------------------- |
| Environment ID      | ENV-002                      |
| Environment Type    | Remote QA / Test Environment |
| Application         | WordPress + WooCommerce      |
| Site Protocol       | HTTPS                        |
| Hosting Platform    | Linux / LiteSpeed            |
| WordPress Version   | 7.0.4                        |
| WooCommerce Version | 11.0.1                       |
| PHP Version         | 7.4.33                       |
| Database            | MySQL 8.0.46                 |
| Language            | en_US                        |
| Currency            | Canadian Dollar (CAD)        |
| Store Region        | Ontario, Canada              |
| Theme               | Twenty Twenty-Five 1.5       |
| Sample Products     | 9                            |
| Baseline Date       | 2026-08-19                   |

> Sensitive infrastructure details, credentials, filesystem paths, database prefixes, and authentication information are intentionally excluded from the public repository.

## 3. WooCommerce Configuration Baseline

### General

| Setting            | Baseline State                       |
| ------------------ | ------------------------------------ |
| Store region       | Canada — Ontario                     |
| Currency           | CAD                                  |
| Currency position  | Left                                 |
| Decimal places     | 2                                    |
| Coupons            | Enabled                              |
| Taxes              | Disabled                             |
| Selling locations  | All countries                        |
| Shipping locations | Countries to which products are sold |

### Checkout and Accounts

| Setting                         | Baseline State |
| ------------------------------- | -------------- |
| Guest checkout                  | Enabled        |
| Account creation after checkout | Available      |
| Password setup link             | Enabled        |
| Personal data retention periods | Not configured |

### Shipping

No shipping zones or shipping methods were configured at the time of baseline capture.

Shipping configuration required by Sprint 1 must therefore be treated as an intentional test-environment change and documented separately.

### Payments

No active payment method was confirmed during baseline capture.

Available providers were presented by WooCommerce, including offline-payment configuration, but an enabled checkout payment method was not established.

Payment configuration required by Sprint 1 must therefore be documented as an intentional environment change.

## 4. Order Storage

High-Performance Order Storage (HPOS) is selected as the active order-storage mechanism.

Observed configuration:

* High-Performance Order Storage selected
* WooCommerce custom order tables enabled
* Active order datastore uses WooCommerce Orders Table storage
* Compatibility synchronization mode not enabled

Database validation during Sprint 1 should therefore be designed against the active HPOS architecture rather than assuming legacy WordPress post-based order storage.

## 5. WooCommerce Pages

The following standard WooCommerce functional areas are available:

* Shop
* Cart
* Checkout
* My Account

A Terms and Conditions page was not configured at baseline.

## 6. Installed Components

WooCommerce is active together with hosting/security-related plugins supplied by the remote hosting environment.

The active WordPress theme is Twenty Twenty-Five. The WooCommerce system report does not declare explicit WooCommerce support for the active theme.

Third-party plugins and theme behaviour will be treated as environmental dependencies if they affect Sprint 1 execution.

## 7. Initial Environment Observations

The following conditions existed before Sprint 1 configuration:

| ID          | Observation                                                            | Initial QA Treatment                                       |
| ----------- | ---------------------------------------------------------------------- | ---------------------------------------------------------- |
| ENV-OBS-001 | Taxes are disabled                                                     | Baseline condition; do not report as defect                |
| ENV-OBS-002 | No shipping method is configured                                       | Test-readiness dependency                                  |
| ENV-OBS-003 | No active payment method was confirmed                                 | Test-readiness dependency                                  |
| ENV-OBS-004 | Guest checkout is enabled                                              | Supports planned guest-checkout testing                    |
| ENV-OBS-005 | Coupons are enabled                                                    | Supports planned promotional testing                       |
| ENV-OBS-006 | HPOS is active                                                         | SQL validation must use appropriate order-storage tables   |
| ENV-OBS-007 | Terms and Conditions page is not configured                            | Out-of-scope unless requirement depends on it              |
| ENV-OBS-008 | Active theme does not declare WooCommerce support in the status report | Monitor for UI/checkout compatibility issues               |
| ENV-OBS-009 | WordPress reports the environment type as production                   | Environment classification to be reviewed before execution |
| ENV-OBS-010 | WordPress Daily Cron is reported as not scheduled                      | Monitor only unless it affects the tested workflow         |

## 8. Test-Readiness Status

**Current Status: NOT READY FOR SPRINT EXECUTION**

The environment is accessible and WooCommerce is operational, but business configuration required for the planned checkout scenario has not yet been completed.

Outstanding test-readiness dependencies:

1. Define Sprint 1 business requirement.
2. Determine whether tax calculation is required by the approved requirement.
3. Configure required shipping method.
4. Configure required offline test payment method.
5. Create controlled QA product data.
6. Create controlled coupon data.
7. Configure WooCommerce REST API credentials when API testing begins.
8. Verify database access for SQL validation.

These items must be introduced as controlled project changes rather than silently treated as part of the original environment baseline.

## 9. Baseline Conclusion

ENV-002 establishes the pre-Sprint state of the remote WooCommerce environment.

This baseline will be used to:

* support test planning;
* identify environment dependencies;
* distinguish configuration issues from product defects;
* provide traceability for intentional Sprint configuration changes; and
* support UI, REST API, and database validation during Sprint execution.

No functional test execution has been performed as part of this baseline activity.
