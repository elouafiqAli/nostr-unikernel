# nostr-unikernel
**Implementation of Nostr in a Unikernel Architecture**

## Goal
To deliver a production-grade Nostr relay implementation that combines high availability, security, affordability, and ease of maintenance.

### Why Nostr?
Nostr, a groundbreaking open protocol, fosters a global, decentralized, and censorship-resistant platform for social media. Its minimalist NIP-01 protocol specification ensures a small footprint, facilitating seamless integration and network participation. Subsequent enhancements and extensions can be introduced as Nostr Implementation Possibilities (NIPs).

### Why Opt for a Unikernel Architecture for a Nostr Relay?
Unikernels enable the execution of programs using only essential system libraries and drivers, translating to lower memory footprints, a condensed stack, and superior performance. Nostr's simplicity is a compelling fit for this model, with the potential to empower anyone to operate a high-availability relay on standard hardware.

### Prospective Technologies for Implementation

Though various unikernel platforms exist, two particularly stand out:

#### Rumprun Kernel (Based on NetBSD)
Developed by Antti Kantee, the rumprun stack utilizes the NetBSD rump kernel, selectively incorporating requisite libraries to execute the desired software stack. This kernel, when combined with the application, behaves as a driver in the system. While the Rump Kernel mandates proficiency in Linux kernel programming, it is versatile, supporting C/C++ Software Stack, Python, JS, and Java. Despite its strength, it carries the overhead of the entire libc stack, often entailing a cluttered library environment. Effective development demands thorough knowledge of the Linux Kernel Development Lifecycle.

#### MirageOS (Powered by OCaml)
Originating from the Xen Hypervisor project and sponsored by Docker, MirageOS is independent of legacy OS constraints, building all drivers and essential libraries from the ground up. OCaml's cohesive development environment, which encompasses various tasks (like configuration, orchestration, and building), offers an integrated approach, eliminating the need for disjointed tools. With credible real-world applications such as Docker Desktop's networking component, MirageOS is a strong contender for sustained, industry-backed unikernel development.

While multiple unikernel stacks are available, the focus, for now, should remain on MirageOS given its consistent development trajectory and widespread industry application.

### Components of the Nostr Relay Unikernel Stack
At a macro level, the stack should encapsulate:
- Nostr relay server.
- Comprehensive installation toolkit.
- Web-based administrative interface.

#### Detailed Work Breakdown

##### Nostr Relay Server
The server should incorporate:
- A dedicated Nostr protocol library (NIP-101).
- An implementation of the Schnorr Secret Sharing using secp256k1.
- Fundamental cryptographic operations (RNG, Zero-Knowledge Proofs, etc.).

The server will be structured as:
- A WebSocket node for internet exposure.
- A data reader node with caching capabilities to access the key-value store.
- A data writer node to modify the key-value store.

Each constituent node functions as a standalone unikernel, leveraging Xen events for inter-node communication.

##### Installation Toolkit
To ensure a scalable and user-friendly deployment, the toolkit should cover:
- A hypervisor installation guide.
- MirageOS + Solo5 setup for maximized portability.
- An Albatross configuration to oversee multiple unikernels.
- Comprehensive guidelines for seamless deployment.

##### Administrative Interface
An all-inclusive, preferably Laravel-based PHP interface is envisioned. This application will interface with Albatross, which in turn connects with the Unikernels. A process-oriented programming paradigm is anticipated, with this interface operating on an independent stack.
