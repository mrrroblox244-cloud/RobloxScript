# ROBLOX Script

---
---

**Viktig1: Player Leaderstats & Respawn Script**

```lua
local Players = game:GetService("Players")

-- NO: Funksjon for å sette opp spillerdata når en spiller blir med i spillet
-- EN: Function to set up player data when a player joins the game
Players.PlayerAdded:Connect(function(player)
	
	-- NO: 1. Opprett leaderstats-mappen for poengtavlen
	-- EN: 1. Create the leaderstats folder for the leaderboard
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

	-- NO: 2. Opprett Stage-verdi for å spore hvilket nivå spilleren er på (starter på 1)
	-- EN: 2. Create Stage value to track player level (starts at 1)
	local stage = Instance.new("IntValue")
	stage.Name = "Stage"
	stage.Value = 1
	stage.Parent = leaderstats

	-- NO: 3. Flytt karakteren til gjeldende sjekkpunkt ved respawn
	-- EN: 3. Teleport character to current checkpoint upon respawn
	player.CharacterAdded:Connect(function(character)
		local currentStage = player.leaderstats.Stage.Value
		local checkpoint = workspace:FindFirstChild("Stage" .. currentStage)

		if checkpoint then
			-- NO: Vent til HumanoidRootPart er lastet inn før teleportering
			-- EN: Wait for HumanoidRootPart to load before teleporting
			local root = character:WaitForChild("HumanoidRootPart")
			task.wait(0.1)
			root.CFrame = checkpoint.CFrame + Vector3.new(0, 3, 0)
		end
	end)
end)
```
---

### 🇳🇴 Norsk (Norwegian)
* **Hva skriptet gjør:** Dette skriptet plasseres i `ServerScriptService` og styrer spillerdata sentralt for hele spillet.
* **Hovedfunksjoner:**
  1. **Poengtavle (leaderstats):** Oppretter automatisk en poengtavle øverst til høyre på skjermen som viser spillernes gjeldende nivå (`Stage`).
  2. **Startverdi:** Alle nye spillere starter automatisk på steg 1 (`Stage = 1`).
  3. **Gjenoppstå (Respawn):** Hver gang en spiller dør og blir født på nytt, sjekker skriptet hvilket nivå de er på, og teleporterer dem direkte til klossen som heter `Stage1`, `Stage2`, osv.
* **Slik setter du det opp:**
  1. Legg skriptet inni **ServerScriptService**.
  2. Gi sjekkpunkt-klossene i verdenen din navn som **`Stage1`**, **`Stage2`**, **`Stage3`** (pass på at **Anchored** er huket av).

---

### 🇬🇧 English
* **What the script does:** Placed in `ServerScriptService`, this script centrally manages player data and respawn locations for the entire server.
* **Key Features:**
  1. **Leaderboard (leaderstats):** Automatically creates a leaderboard in the top-right corner showing each player's current `Stage`.
  2. **Starting Stage:** Every player starts at level 1 by default (`Stage = 1`).
  3. **Automatic Respawn:** Whenever a player dies, the script checks their current stage number and teleports their character directly to the corresponding checkpoint part (`Stage1`, `Stage2`, etc.).
* **How to set it up:**
  1. Put the script inside **ServerScriptService**.
  2. Name your checkpoint parts in the Workspace as **`Stage1`**, **`Stage2`**, **`Stage3`**, etc. (Make sure **Anchored** is set to `true`).

---

### 🇺🇦 Українська (Ukrainian)
* **Що робить скрипт:** Скрипт розміщується у `ServerScriptService` і централізовано керує даними гравців та точками появи на сервері.
* **Основні функції:**
  1. **Таблиця лідерів (leaderstats):** Автоматично створює таблицю лідерів у правому верхньому кутку екрана, яка відображає поточний рівень гравця (`Stage`).
  2. **Початковий рівень:** Усі нові гравці автоматично починають з 1-го рівня (`Stage = 1`).
  3. **Відродження (Respawn):** Щоразу, коли гравець гине та з'являється знову, скрипт перевіряє його поточний рівень і телепортує персонажа до відповідного блоку-чекпоінта (`Stage1`, `Stage2` тощо).
* **Як налаштувати:**
  1. Помістіть скрипт усередину **ServerScriptService**.
  2. Назвіть блоки чекпоінтів у Workspace як **`Stage1`**, **`Stage2`**, **`Stage3`** (переконайтеся, що прапорець **Anchored** увімкнено).

---

### 🇹🇭 ไทย (Thai)
* **หน้าที่ของสคริปต์:** สคริปต์นี้ใส่ไว้ใน `ServerScriptService` เพื่อใช้ควบคุมข้อมูลผู้เล่นและการเกิดใหม่จากส่วนกลางของเซิร์ฟเวอร์
* **คุณสมบัติหลัก:**
  1. **ตารางคะแนน (leaderstats):** สร้างกระดานคะแนนมุมขวาบนของหน้าจอโดยอัตโนมัติ เพื่อแสดงระดับด่านปัจจุบัน (`Stage`) ของผู้เล่นแต่ละคน
  2. **ค่าเริ่มต้น:** ผู้เล่นทุกคนที่เข้าเกมมาใหม่จะเริ่มที่ด่าน 1 เสมอ (`Stage = 1`)
  3. **การวาร์ปเมื่อเกิดใหม่ (Respawn):** ทุกครั้งที่ผู้เล่นตายแล้วเกิดใหม่ สคริปต์จะเช็กว่าผู้เล่นอยู่อันดับด่านที่เท่าไร แล้วย้ายตัวละครไปเกิดบนแผ่น Checkpoint ที่ตั้งชื่อว่า `Stage1`, `Stage2` ฯลฯ ทันที
* **วิธีติดตั้ง:**
  1. นำสคริปต์นี้ไปใส่ไว้ใน **ServerScriptService**
  2. ตั้งชื่อแผ่น Checkpoint ในฉาก (`Workspace`) ให้เป็น **`Stage1`**, **`Stage2`**, **`Stage3`** ตามลำดับ (และอย่าลืมเปิด **Anchored** = `true`)
 
---
---

**Viktig2: Checkpoint Script (Sjekkpunkt / Контрольна точка / จุดบันทึกจุดเกิด)**

- 🇬🇧: Updates the player's spawn location to this block upon touch.
- 🇳🇴: Oppdaterer spillere-s spawn-lokasjon til denne klossen ved berøring.
- 🇺🇦: Змінює точку появи гравця на цей блок при доторку.
- 🇹🇭: อัปเดตจุดเกิดของผู้เล่นมาที่แผ่นนี้เมื่อสัมผัส

```lua
local checkpoint = script.Parent

checkpoint.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player then
		player.RespawnLocation = checkpoint
	end
end)
```

***How to set it up in Roblox Studio:***

1. Insert a Part where you want the checkpoint to be.
2. In the Properties window, make sure Anchored is set to true.
3. Insert a standard Script inside that Part and paste the code above.

***Slik setter du det opp i Roblox Studio:***

1. Sett inn en Part: Legg til en Part (kloss) der du vil at sjekkpunktet skal være.
2. Fest klossen (Anchored): I vinduet for Properties (Egenskaper), pass på at Anchored er huket av (true) slik at klossen ikke faller ned.
3. Legg til skript: Legg til et vanlig Script inni denne klossen og lim inn koden.

---
---

1. **Kill Block (Dødskloss / Смертельний блок / แผ่นอันตราย)**

- 🇬🇧: Instantly kills the player upon touch.
- 🇳🇴: Dreper spilleren umiddelbart ved berøring.
- 🇺🇦: Миттєво вбиває гравця при доторку.
- 🇹🇭: ทำให้ตัวละครตายทันทีเมื่อสัมผัส

```lua
local killBlock = script.Parent

killBlock.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.Health = 0
	end
end)
```

---
---

2. **Disappearing Block (Forsvinnende kloss / Зникаючий блок / แผ่นหายตัว)**

- 🇬🇧: Block becomes invisible and non-solid shortly after being touched.
- 🇳🇴: Klossen blir usynlig og umulig å stå på en kort stund etter berøring.
- 🇺🇦: Блок стає невидимим і не проходить крізь нього короткий час після доторку.
- 🇹🇭: แผ่นจะจางหายและทะลุได้ชั่วคราวเมื่อเหยียบ

```lua
local part = script.Parent
local isTouched = false

part.Touched:Connect(function()
	if not isTouched then
		isTouched = true
		task.wait(0.3)
		part.Transparency = 0.8
		part.CanCollide = false
		task.wait(2)
		part.Transparency = 0
		part.CanCollide = true
		isTouched = false
	end
end)
```

---
---

3. **Speed Boost (Fartsøkning / Прискорення / แผ่นเพิ่มความเร็ว)**

- 🇬🇧: Temporarily increases the player's walking speed.
- 🇳🇴: Gir spilleren raskere gåfart midlertidig.
- 🇺🇦: Тимчасово збільшує швидкість ходьби гравця.
- 🇹🇭: เพิ่มความเร็วในการเดินชั่วคราว

```lua
local speedPad = script.Parent

speedPad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid and humanoid.WalkSpeed == 16 then
		humanoid.WalkSpeed = 40
		task.wait(3)
		humanoid.WalkSpeed = 16
	end
end)
```

---
---

4. **High Jump Pad (Hoppepute / Стрибкова подушка / แผ่นเด้งสูง)**

- 🇬🇧: Launches the player into the air using a velocity vector.
- 🇳🇴: Sender spilleren opp i luften med en hastighetsvektor.
- 🇺🇦: Підкидає гравця в повітря за допомогою вектора швидкості.
- 🇹🇭: ส่งตัวละครกระโดดลอยขึ้นฟ้าด้วยเวกเตอร์ความเร็ว

```lua
   local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	if root then
		root.Velocity = Vector3.new(0, 80, 0)
	end
end)
```

---
---

5. **Rotating Obstacle (Roterende hindring / แท่งหมุนสิ่งกีดขวาง)**

- 🇬🇧: Continuously rotates the part around its axis.
- 🇳🇴: Roterer klossen kontinuerlig rundt sin akse.
- 🇺🇦: Безперервно обертає блок навколо своєї осі.
- 🇹🇭: หมุนชิ้นส่วนไปเรื่อยๆ อย่างต่อเนื่อง

```lua

local part = script.Parent

while true do
	part.CFrame = part.CFrame * CFrame.Angles(0, math.rad(5), 0)
	task.wait(0.03)
end
```

---

6. **Teleporter (Teleportering / วาร์ปไปจุดต่อไป)**

- 🇬🇧: Instantly moves the player to a target location in the game world.
- 🇳🇴: Flytter spilleren umiddelbart til et annet mål i spillverdenen.
- 🇺🇦: Миттєво переміщує гравця до іншої цілі у світі гри.
- 🇹🇭: ย้ายตำแหน่งตัวละครไปยังจุดปลายทางทันที

```lua
local portal = script.Parent

portal.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	local target = workspace:FindFirstChild("TeleportTarget")
	
	if root and target then
		root.CFrame = target.CFrame + Vector3.new(0, 3, 0)
	end
end)
```

---
---

7. **Lava Floor (Lava-gulv / Лавова підлога / แผ่นลาวาค่อยๆ ลดเลือด)**

- 🇬🇧: Gradually damages the player while standing on the block.
- 🇳🇴: Skader spilleren gradvis så lenge de står på klossen.
- 🇺🇦: Поступово завдає шкоди гравцю, поки він стоїть на блоці.
- 🇹🇭: ค่อยๆ ลดเลือดเรื่อยๆ ตราบใดที่ยังยืนบนแผ่นนี้

```lua
local lavaPart = script.Parent

lavaPart.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid and humanoid.Health > 0 then
		humanoid:TakeDamage(10)
		task.wait(0.5)
	end
end)
```

---

8. **Conveyor Belt (Samlebånd / Конвеєрна стрічка / สายพานเลื่อนตัวละคร)**

- 🇬🇧: Automatically pushes the player in a specific direction.
- 🇳🇴: Skyver spilleren i en bestemt retning automatisk.
- 🇺🇦: Автоматично штовхає гравця в певному напрямку.
- 🇹🇭: ดันตัวละครให้เคลื่อนที่ไปตามทิศทางอัตโนมัติ

```lua
local conveyor = script.Parent

conveyor.AssemblyLinearVelocity = conveyor.CFrame.LookVector * 25
```

---
---

9. **Trampoline (Super-trampoline / Батут / แผ่นสปริงเด้งดึ๋ง)**

- 🇬🇧: Launches the player upward using an impulse force.
- 🇳🇴: Skyter spilleren oppover ved hjelp av impuls-kraft.
- 🇺🇦: Підкидає гравця вгору за допомогою імпульсної сили.
- 🇹🇭: ดีดตัวผู้เล่นขึ้นด้านบนด้วยแรงกระแทก

```lua
local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	if root then
		root:ApplyImpulse(Vector3.new(0, 2500, 0))
	end
end)
```

---
---

10. **Coin Collector (Mynt-samler / Збір монет / เหรียญเก็บสะสม)**

- 🇬🇧: Awards points to the player and temporarily vanishes before respawning.
- 🇳🇴: Gir poeng til spilleren og forsvinner midlertidig før den dukker opp igjen.
- 🇺🇦: Нараховує очки гравцю та тимчасово зникає перед відновленням.
- 🇹🇭: เพิ่มคะแนนให้ผู้เล่นและเหรียญจะหายไปชั่วคราวก่อนเกิดใหม่

```lua
local coin = script.Parent
local isCollected = false

coin.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player and not isCollected then
		isCollected = true
		if player:FindFirstChild("leaderstats") and player.leaderstats:FindFirstChild("Coins") then
			player.leaderstats.Coins.Value += 1
		end
		coin.Transparency = 1
		coin.CanCollide = false
		task.wait(5)
		coin.Transparency = 0
		coin.CanCollide = true
		isCollected = false
	end
end)
```

---
---

11. **Falling Floor (Fellende gulv / Падаюча підлога / พื้นใต้เท้าหล่น)**

- 🇬🇧: The floor unanchors and falls down when stepped on.
- 🇳🇴: Gulvet mister forankringen og faller ned når spilleren tråkker på det.
- 🇺🇦: Підлога втрачає закріплення і падає, коли на неї наступають.
- 🇹🇭: พื้นจะหลุดร่วงตกลงมาเมื่อผู้เล่นเหยียบ

```lua
local trapDoor = script.Parent
local triggered = false

trapDoor.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	if character:FindFirstChildOfClass("Humanoid") and not triggered then
		triggered = true
		task.wait(0.5)
		trapDoor.Anchored = false
		task.wait(3)
		trapDoor.AssemblyLinearVelocity = Vector3.zero
		trapDoor.AssemblyAngularVelocity = Vector3.zero
		trapDoor.Anchored = true
		triggered = false
	end
end)
```

---
---

12. **Checkpoint Flag (Sjekkpunkt-flagg / Прапорець збереження / ธงบันทึกจุดเกิด)**

- 🇬🇧: Updates the player's spawn location to this block upon touch
- 🇳🇴: Endrer spillerens spawn-lokasjon til denne klossen ved berøring.
- 🇺🇦: Змінює точку появи гравця на цей блок при доторку..
- 🇹🇭: อัปเดตจุดเกิดของผู้เล่นมาที่แผ่นนี้เมื่อสัมผัส

```lua
local checkpoint = script.Parent

checkpoint.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player then
		player.RespawnLocation = checkpoint
	end
end)
```

---
---

13. **Low Gravity Zone (Lav tyngdekraft / Зона низької гравітації / โซนแรงโน้มถ่วงต่ำ)**

- 🇬🇧: Temporarily allows the player to jump much higher.
- 🇳🇴: Gir spilleren mulighet til å hoppe mye høyere midlertidig.
- 🇺🇦: Дозволяє гравцеві стрибати набагато вище тимчасово.
- 🇹🇭: ทำให้ผู้เล่นกระโดดได้สูงขึ้นมากชั่วคราว

```lua
local zone = script.Parent

zone.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.UseJumpPower = true
		humanoid.JumpPower = 100
	end
end)
```

---
---

14. **Reset Jump Pad (Nullstill hopp / Скидання стрибка / แผ่นรีเซ็ตการกระโดด)**

- 🇬🇧: Resets the player's jump power back to the default value.
- 🇳🇴: Tilbakestiller spillerens hoppekraft til standardverdi.
- 🇺🇦: Повертає силу стрибка гравця до стандартного значення.
- 🇹🇭: คืนค่าพลังการกระโดดของผู้เล่นให้กลับมาเป็นค่าปกติ

```lua
local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 50
	end
end)
```

---
---

15. **Blinking Block (Blinkende kloss / Миготливий блок / แผ่นกะพริบเปิด-ปิด)**

- 🇬🇧: Automatically toggles visibility and collision at regular time intervals.
- 🇳🇴: Veksler automatisk mellom å være synlig og usynlig med faste mellomrom.
- 🇺🇦: Автоматично перемикається між видимим і невидимим через рівні проміжки часу.
- 🇹🇭: สลับสถานะการแสดงผลและการชนตามเวลาที่กำหนดโดยอัตโนมัติ

```lua
local part = script.Parent

while true do
	part.Transparency = 0
	part.CanCollide = true
	task.wait(2)
	part.Transparency = 1
	part.CanCollide = false
	task.wait(2)
end
```

---
---

16. **Color Changing Block (Fargeskiftende kloss / Блок, що змінює колір / แผ่นเปลี่ยนสีสุ่ม)**

- 🇬🇧: Randomly changes the block's color every time it is touched.
- 🇳🇴: Endrer klossens farge tilfeldig hver gang den berøres.
- 🇺🇦: Змінює колір блоку випадковим чином щоразу при доторку.
- 🇹🇭: สุ่มเปลี่ยนสีของแผ่นทุกครั้งที่มีคนสัมผัส

```lua
local part = script.Parent

part.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	if character:FindFirstChildOfClass("Humanoid") then
		part.Color = Color3.fromRGB(math.random(0, 255), math.random(0, 255), math.random(0, 255))
	end
end)
```

---
---

17. **Push Back Wall (Skyve-vegg / Стіна відштовхування / กำแพงผลักถอยหลัง)**

- 🇬🇧: Knocks the player backward in the opposite direction they are facing.
- 🇳🇴: Dytter spilleren bakover i motsatt retning av der den ser.
- 🇺🇦: Відштовхує гравця назад у протилежному напрямку від його погляду.
- 🇹🇭: ผลักตัวละครให้กระเด็นถอยหลังสวนทางกับทิศทางที่หันหน้าไป

```lua
local wall = script.Parent

wall.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	if root then
		root:ApplyImpulse(root.CFrame.LookVector * -1500)
	end
end)
```

---
---

18. **Heal Pad (Helbredende kloss / Блок лікування / แผ่นเพิ่มเลือดเต็ม)**

- 🇬🇧: Restores the player's health to maximum upon touch.
- 🇳🇴: Fyller opp spillerens helse til maksimum når den berøres.
- 🇺🇦: Відновлює здоров'я гравця до максимуму при доторку.
- 🇹🇭: ฟื้นฟูพลังชีวิตของผู้เล่นให้เต็มทันทีเมื่อสัมผัส

```lua
local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.Health = humanoid.MaxHealth
	end
end)
```

---
---

19. **Speed Slowdown Pad (Saktegående kloss / Блок сповільнення / แผ่นลดความเร็วเดินช้า)**

- 🇬🇧: Temporarily slows down the player's movement speed as a hazard.
- 🇳🇴: Sakker ned spillerens hastighet midlertidig som en straff-sone.
- 🇺🇦: Тимчасово сповільнює швидкість гравця як штрафна зона.
- 🇹🇭: ลดความเร็วในการเดินของผู้เล่นลงชั่วคราวเหมือนโดนกับดักหน่วง

```lua
local slowPad = script.Parent

slowPad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid and humanoid.WalkSpeed == 16 then
		humanoid.WalkSpeed = 6
		task.wait(3)
		humanoid.WalkSpeed = 16
	end
end)
```

---
---

20. **Invisible Kill Block (Usynlig dødskloss / Невидимий смертельний блок / แผ่นอันตรายล่องหน)**

- 🇬🇧: A completely invisible trap block that kills the player without warning.
- 🇳🇴: En helt usynlig fellekloss som dreper spilleren uten forvarsel.
- 🇺🇦: Повністю невидимий блок-пастка, який вбиває гравця без попередження.
- 🇹🇭: แผ่นอันตรายที่มองไม่เห็นตัวตน (โปร่งใส 100%) ใช้ดักผู้เล่นไม่ให้รู้ตัว

```lua
local secretKill = script.Parent
secretKill.Transparency = 1
secretKill.CanCollide = true

secretKill.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.Health = 0
	end
end)
```

---
---


