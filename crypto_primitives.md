## **NIP-01 Cryptographic Library for MirageOS**

---

### **Introduction:**

We aim to create an OCaml library tailored for the MirageOS unikernel, implementing the cryptographic requirements specified by NIP-01.

---

### **Table of Contents:**

1. Requirements & Primitives Identification
2. Library Development
3. Testing
4. Optimization & Documentation
5. Release & Maintenance
6. Contribution Guidelines

---

### **1. Requirements & Primitives Identification:**

- **SHA-256**:
  - Use the `nocrypto` library available in MirageOS.

- **Schnorr signatures**:
  - Research available libraries for compatibility with MirageOS.
  - Plan for custom implementation if no suitable libraries are found.

---

### **2. Library Development:**

- **Key Pair Management**:
    - `signId(privkey, id)`, `verifyEvent(event)`, `getPublicKey(privkey)`.
    
- **Event ID Creation**:
    - `calculateId(ev)`: Utilize `nocrypto`.

- **Signing Event Data**:
    - `signDelegationToken(privkey, unsigned_token)`: Combine `nocrypto` with Schnorr's signing.

- **Encryption**:
    - `encryptDm(privkey, to, msg)`: Leverage `nocrypto`.

---

### **3. Testing:**

- **Unit Tests**:
  - Generate sample data.
  - Test every function using tools like `alcotest`.

- **Integration Tests**:
  - Ensure correct function interactions within the NIP-01 protocol.

- **Benchmarking**:
  - Measure speed and memory using the `benchmark` OCaml library.

---

### **4. Optimization & Documentation:**

- **Optimization**:
  - Optimize based on benchmarking feedback.
  
- **Documentation**:
  - Detailed comments for each function.
  - Utilize `odoc` for API documentation.

---

### **5. Release & Maintenance:**

- **Release**:
  - Package with `opam`.
  - Provide installation and usage guidelines.

- **Maintenance**:
  - Use GitHub issues for feedback and bug tracking.
  - Periodic updates addressing bugs, optimizations, or NIP-01 spec changes.

