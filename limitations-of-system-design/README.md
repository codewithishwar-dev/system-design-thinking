# 💡 Limitations of System Design (with Real-World Examples)

System design is often presented as clean diagrams and perfect architectures.

But in reality, every system is built on **trade-offs**.

---

## 🚫 Key Limitations

### 1. No Design is Future-Proof
- Systems evolve with scale
- What works today may break tomorrow

📌 Example:
- Netflix started with a monolith and later moved to microservices as user scale increased

👉 Real-world:
Your simple backend works fine… until traffic grows unexpectedly

---

### 2. Trade-offs are Unavoidable
- You cannot optimize everything at once

📌 Example:
- Amazon often prioritizes availability over strict consistency  
- Users may see "Order Placed" even when backend systems are still syncing

👉 Real-world:
Fast user experience is often preferred over perfect accuracy

---

### 3. Over-Engineering Kills Speed
- Microservices are not always the answer

👉 Real-world:
Many teams split into multiple services too early → slows development

---

### 4. Assumptions Can Fail
- Traffic patterns and user behavior change

📌 Example:
- Uber had to redesign its dispatch and surge pricing systems as demand evolved

👉 Real-world:
Your system assumptions break as product usage grows

---

### 5. Cost vs Performance
- Better performance requires more resources

👉 Real-world:
Caching, CDNs, and replication improve speed but increase infrastructure cost

---

### 6. Complexity Increases with Scale
- More services = more complexity

👉 Real-world:
Debugging distributed systems is harder than building them

---

## 🎯 Key Takeaway

> There is NO perfect system design  
> Only better trade-offs based on your current needs

---

## 📌 Author

**CodeWithIshwar | Ishwar Chandra Tiwari**  
Backend Developer | Learning in Public 🚀  

---

## ⭐ Support

If you found this useful, consider giving a ⭐ to the repo!
