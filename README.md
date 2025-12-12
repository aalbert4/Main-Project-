# 🎮 Om Nom: Catch the orbs

## 📌 Overview
**Om Nom: Rope Cut** is a 2D physics-based reaction and sides scroller game inspired by *Cut the Rope*.  
Your goal is simple: **catch falling orbs, avoid harmful ones, and survive as long as possible**.

This game is built in **Unreal Engine 5.4.4**, using **Paper2D**, physics constraints, Blueprints, and a dynamic UI system.

---

## 🕹️ Gameplay

### 🎯 Objective
Catch normal orbs to earn points and avoid damaging orbs that destroy lives.  
Missing normal orbs reduces lives and score.  
Catching special orbs grants temporary power-ups.
Catching damaging orbs reduces only your life

---

## 🍬 Orb Types

### *Source*
Orb Sprites and it's variation were generated with ChatGpt 

https://chatgpt.com/share/68f81730-c4c4-8003-8bc7-ac57d5c3625b 

### **Normal Orb**
- Grants **+10 score** (or more with multipliers)
- Plays Om Nom's **eat animation**
- Missing it:
  - **–1 life**
  - **–10 score**
  - Plays miss sound effect
  - Triggers screen shake

### ⭐ **Special Orb**
- Rare random spawn  
- Grants temporary effects:
  - **Score Multiplier x2**
  - **Increased movement speed**
  - **Visual indicator** (green glow)
- Effect lasts **5 seconds**
- Missing it has **no penalty**
- Catching special orbs never reduce score or lives

### 💀 **Damaging Orb**
- Catching it:
  - **–1 life**
  - Plays **Om nom's throw-up animation**
  - Plays damage sound
  - Triggers screen shake
- Missing it has **no effect**

---

## 👾 Player (Om Nom)


### *Source*
Om Nom and it's variety sprites were generated with ChatGpt https://chatgpt.com/s/m_693c8c84ab3081919d087c562182b578 

### **Movement**
- Controlled with **Left/Right keyboard inputs**
- Speed = `MoveSpeed * SpeedMultiplier`
- Bound to the playable screen width using Clamp nodes

### **Animations**
Om Nom has multiple PaperFlipbook animations:
- **Idle**
- **Eat**
- **Throw-up**
- States controlled by:
  - IsEating
  - IsThrowingUp

Animations automatically return to **Idle** when done.

---

## 🔊 Audio
### *Source*
https://github.com/yell0wsuit/CutTheRope/tree/master/audio 

The game features:
- Candy catch sound  
- Candy break/miss sound (audio_candy_break)
- Power-up activation sound  
- Damage sound  
- 3 Classical **cut the rope music system**:
  - Tracks cycle automatically using an index
  - When one track ends, the next plays
  - Loops back to track 0 at the end

---

## 📸 Camera Effects

To enhance gameplay experience, I created:
- **Screen shake** when missing a normal orb  
- **Screen shake** when catching a damaging orb  
- Uses a custom CameraShake class

---

## 🧠 Game Systems

### ⭐ Scoring
- Score increases when catching orbs
- Special orb enables ScoreMultiplier = 2 which increases player points by 20 for 5 seconds
- Score resets properly back to normal after the effect ends
- Score never decreases for missing special/damaging orbs

### ❤️ Lives
- Player starts with 3 Lives
- Missed normal orb → lose 1 life  
- Caught damaging orb → lose 1 life  
- Special golden orb never affects lives negatively  
- Lives auto-update on the UI  
- Bonus life awarded when reaching a specific score threshold (200)

### 🔥 Special Orb Timer
Uses SetTimerByFunctionName:
- Activates speed boost  
- Activates score multiplier  
- Shows visual indicator  
- Resets both after 5 seconds  

### 🧪 Orb Collision Handling
Each orb blueprint handles:
- Overlap detection with Om Nom  
- Miss detection based on falling past MissZ  
- Passing orb category to LevelController for scoring and life logic  

---

## 💡 UI System

The HUD includes:
- **Score display**  
- **Lives display**  
- **Special orb active indicator**

## 💔 GameOver System

After losing all 3 (or 4) lives it's game over: 
- **Game over UI displays**
- **Movement and everything else gets restricted**
- **Music still plays**
- **Pressing enter restarts the game**