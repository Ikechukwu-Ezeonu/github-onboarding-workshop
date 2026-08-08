# My Notes — Elu Uchenna Emmanuel

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- Azure storage services, the access tiers and redundancy option available 
- Gained more insight into blobs, files, queues and tables 
- AZ storage is durable and highly available, its is encrypted by default, scalable and globally accessible
- Create Storage, blobs, files etc. define access policy and SAS.

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did
- Created a storage account, define redundancy, access tiers and disabled anonymous public access.
  <img width="1503" height="669" alt="Screenshot 2026-08-07 124351" src="https://github.com/user-attachments/assets/6f627c37-2176-4275-ad9a-b58f24341406" />
- Downloaded storage explorer for testing
- Provide access to a blob using SAS
  <img width="785" height="399" alt="Screenshot 2026-08-07 125548" src="https://github.com/user-attachments/assets/9946825e-b1f6-4f49-9933-7f16a4b575a6" />
- Also created access policy for blobs
  <img width="1349" height="623" alt="image" src="https://github.com/user-attachments/assets/63eb7069-ed8d-4bdd-90fe-06353913227a" />
- Connected to the storage account using access keys and test it using storage explorer. This approach will grant access to the entire storage account which is not best practice.
  <img width="1776" height="882" alt="image" src="https://github.com/user-attachments/assets/766a76f8-cf7d-40e2-b47b-1f1dedba2ea1" />
- Connected to the storage account using SAS. With this approach, you can limit the access to the service they require and the permission and the duration of the access.
  <img width="1494" height="878" alt="image" src="https://github.com/user-attachments/assets/83fcb59f-63f4-49d3-aedb-478dc7acfcba" />
  <img width="1890" height="754" alt="image" src="https://github.com/user-attachments/assets/ce7b6909-fa1e-45c9-a6b6-677f1535f8ff" />
- Rotated the key to disable any existing access to the storages
  
### What happened / Result
- With anonymous access disabled, below is the outcome.
  <img width="1731" height="415" alt="image" src="https://github.com/user-attachments/assets/77dbeb9f-6772-4d69-990c-6bfad2a2118c" />
- Only access to the blob was possible using SAS to limit access to blob only
  <img width="1890" height="754" alt="image" src="https://github.com/user-attachments/assets/798920f0-6a4e-4ff6-8fa6-3f5e44c07fb3" />
- Authentication error occurred after rotating the key 
  <img width="804" height="459" alt="Screenshot 2026-08-07 134229" src="https://github.com/user-attachments/assets/2fe4566e-f107-4b3d-8405-36c05565ac82" />

### Challenges I faced
- None

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
- Always ensure you have a clear understanding of the reason behind setting up the storage account and apply necessary security measures like disabling public access to the storage account, to reduce the attack surface.
- Securing Azure Storage by implementing the right combination of identity, network, and data controls to ensure confidentiality, integrity, and availability.
---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- https://www.youtube.com/watch?v=HKW1jYi9wKE
- https://learn.microsoft.com/en-us/training/paths/implement-azure-storage-security/

---

*Submitted by: Elu Uchenna Emmanuel · eluemma*
