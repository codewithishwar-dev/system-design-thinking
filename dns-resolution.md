# 🌐 DNS Resolution (How the Internet Finds IP Addresses)

When you type a URL like:

```
www.google.com
```

Your system does not know the IP address directly.
It uses the **Domain Name System (DNS)** to resolve it.

---

## 🔁 Step-by-Step Process

1. **Check Local Cache**

   * Browser cache
   * OS cache
     👉 If found → instant response

2. **Query DNS Resolver**

   * Provided by ISP or public DNS (e.g., Google DNS)

3. **Resolver Queries Hierarchy**

   * Root Server → points to TLD
   * TLD Server (.com) → points to domain
   * Authoritative Server → returns actual IP

4. **Cache the Result**

   * Stored with TTL (Time To Live)

---

## 🧠 Core Concepts

* 🌳 Tree Traversal (Root → TLD → Domain)
* 🔁 Recursive + Iterative Resolution
* ⚡ Heavy Caching (performance booster)
* 🧩 Hash-based lookup (inside DNS servers)

---

## ⚡ Performance Insight

* Without caching → multiple network hops
* With caching → near O(1) lookup

👉 This is why DNS feels instant.

---

## 🚨 Real Engineering Insight

DNS is not just a lookup system.

It is designed to:

* Handle billions of requests
* Maintain low latency
* Ensure high availability

---

## 🔥 Key Takeaway

> DNS is a globally distributed, cached lookup system optimized for speed and scale.

---

## 🏷️ Tags

`dns` `system-design` `networking` `backend` `scalability` `performance`

---

- CodeWithIshwar | Ishwar Chandra Tiwari
