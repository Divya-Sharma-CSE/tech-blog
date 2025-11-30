# Entropy From Lava Lamps: How Cloudflare Generates Randomness

> A beginner-friendly breakdown of how colorful lava lamps help secure millions of websites.

---

## 🔥 1. Why Lava Lamps?

Short intro explaining unpredictability + analog chaos.

---

## 📸 2. How Cloudflare Captures Entropy

!!! note
    Entropy = randomness collected from the environment.

- Camera captures lamp wall
- Converts into pixel noise
- Hashes are computed

---

## 🧪 3. Turning Chaos Into Secure Randomness

```mermaid
flowchart TD
    A[Lava Lamps] --> B[Camera]
    B --> C[Hash Function]
    C --> D[Entropy Pool]
    D --> E[CSPRNG Output]
