# Boundary — Agency Framework vs This SaaS

**Agency framework:** reusable process for *different* client software projects. Each bespoke client usually receives isolated source/infra, subject to written ownership and hosting terms.

**AC Service Manager:** one agency-owned product shared by independent AC businesses with tenant isolation, product-level roadmap and subscription/usage settings. The AC company invites its own staff but never accesses other companies' records, your source code or infrastructure secrets. Agency platform operators see operational state by default, not all customer personal data.

If first prospective client wants ownership of a custom implementation or demands integration with an unsupported proprietary tool, document whether that is a bespoke engagement, product feature or paid connector. Do not accidentally turn the SaaS into a private custom-code fork without business approval.

Repo split: `agency-engineering-framework` is generic; `ac-service-manager` is product-specific. Never copy client data or secrets into framework templates.
