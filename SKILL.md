---
name: video-promt
description: Tài liệu quy chuẩn cấu trúc câu lệnh (Prompt) tạo video đa phương thức (Text + Image + Video + Audio)
---
## 1. NGUYÊN TẮC CỐT LÕI & CÚ PHÁP THAM CHIẾU (`@Image`, `@Video`, `@Audio`)

### 1.1. 4 Nguyên tắc Vàng (Golden Rules)
1. **Quy tắc `1 File = 1 Vai trò`:** Khi đã tải file lên, KHÔNG mô tả lại ngoại hình hay bối cảnh bằng chữ. Chỉ định rõ mô hình cần lấy yếu tố nào từ file nào.
2. **Độ dài tối ưu:** Giữ prompt trong khoảng **50 – 90 từ** (hoặc 1 cấu trúc Hybrid JSON gọn) để mô hình xử lý vật lý và ánh sáng chuẩn nhất.
3. **Đồng bộ thời lượng đầu vào:** Cắt độ dài của `@Video` gốc và `@Audio` thoại bằng nhau (ví dụ: cùng 6s, 8s hoặc 10s) trước khi tải lên để khớp tốc độ mấp máy môi (lip-sync).
4. **Bảo vệ chi tiết sản phẩm (Asset Lock):** Luôn yêu cầu góc máy tĩnh hoặc đẩy nhẹ (`slow push-in`) và cầm vào cạnh/đáy sản phẩm (`gripping the side/bottom without covering key logos`) để không làm nhòe chữ hoặc logo trên bao bì.

### 1.2. Từ điển Gán vai trò File Tham chiếu (Reference Syntax)

| Loại File | Vai trò | Cú pháp chuẩn (Tiếng Anh) |
| :--- | :--- | :--- |
| **`@Image` (Sản phẩm)** | Khóa hình dáng, màu sắc, logo và nhãn mác | `Use @Image1 as the exact product reference, preserving silhouette, color scheme, logo placement, and label graphics.` |
| **`@Image` (Nhân vật)** | Khóa khuôn mặt, kiểu tóc, trang phục | `Use the person in @Image1 as the character reference, maintaining exact facial identity, hairstyle, and outfit.` |
| **`@Image` (Bối cảnh)** | Khóa môi trường / không gian không gian mẫu | `Place the scene inside the exact environment and lighting conditions shown in @Image2.` |
| **`@Video` (Motion Ref)** | Lấy cử chỉ, dáng đứng, góc máy (dùng khi **Create**) | `Apply the body posture, hand gestures, and handheld camera movement from @Video1 to the character.` |
| **`@Video` (Base Canvas)** | Giữ nguyên video gốc để đè vật thể/người (dùng khi **Edit**) | `Use @Video1 as the base video: keep exact background, lighting, camera movement, and unedited segments.` |
| **`@Audio` (Voiceover)** | Khóa giọng đọc & đồng bộ khẩu hình (Lip-sync) | `Use @Audio1 as the voice track. Synchronize lip movements, jaw motion, and facial expressions to @Audio1.` |

---

# PHẦN I: CREATE VIDEO (TẠO VIDEO MỚI TỪ ĐẦU)

Dùng khi bạn **tạo ra một cảnh quay hoàn toàn mới** từ văn bản kết hợp các nguyên liệu rời rạc (Ảnh nhân vật + Ảnh sản phẩm + Video mẫu chuyển động + File thu âm).

## 2.1. Công thức Tổng quát Create Video (6 Lớp)

```text
[1. Format & Shot Control] + [2. Reference Roles (@Image/@Video/@Audio)] + [3. Scene & Timed Action] + [4. Camera & Lighting] + [5. Audio & Lip-Sync] + [6. Strict Constraints]
```

## 2.2. Các Mẫu Text Prompt – Create Video

### Mẫu Create 1: Tạo Video Kỹ sư/Nông dân cầm sản phẩm tư vấn tại vườn (`@Image1` + `@Image2` + `@Video1` + `@Audio1`)
* **Đầu vào:** `@Image1` (Ảnh nhân vật) + `@Image2` (Ảnh chai thuốc/phân bón) + `@Video1` (Video mẫu lấy chuyển động tay) + `@Audio1` (File giọng đọc).
```text
Create a 10-second vertical marketing video in a single continuous shot, no scene cuts.
1. Reference Roles: Use the character from @Image1 as the agricultural engineer, keeping his face, hairstyle, and polo shirt consistent. Use the bottle in @Image2 as the exact product reference. Apply the body posture, hand gestures, and subtle handheld camera movement from @Video1 to the engineer.
2. Scene & Action: The engineer stands in a lush green durian orchard under warm morning sunlight. [0-3s] He points toward a fruiting branch, [3-10s] then holds the product bottle from @Image2 steadily at chest level toward the camera with a confident nod.
3. Camera & Lighting: Medium close-up shot, shallow depth of field blurring the orchard background, natural sunlight hitting the leaves and bottle surface.
4. Audio & Lip-Sync: Use @Audio1 as the primary voice track and synchronize the engineer's lip movements and facial expressions to the speech, layered with subtle orchard wind ambience.
5. Constraints: Keep the bottle shape, cap color, label design, and logo from @Image2 completely unchanged. Ensure 5 natural fingers gripping the side of the bottle without covering the front label.
```

### Mẫu Create 2: Tạo Video Hook 2 Cảnh – Triệu chứng Bệnh hại $\rightarrow$ Reveal Sản phẩm (`@Image1` + `@Image2` + `@Audio1`)
* **Đầu vào:** `@Image1` (Ảnh lá bệnh/rụng bông) + `@Image2` (Ảnh sản phẩm) + `@Audio1` (Âm thanh cảnh báo + Voiceover).
```text
Create a 6-second vertical social ad with two timed shots synchronized to @Audio1.
- Shot 1 [0-3s]: Macro close-up based on @Image1 showing diseased leaves swaying in wind and rain, overcast dramatic lighting, fast handheld push-in creating urgency.
- Shot 2 [3-6s]: Clean hero reveal shot of the agricultural product from @Image2 standing on a wooden post in a healthy sunlit green field. Slow smooth push-in toward the product, water droplets glistening on the packaging.
Audio: Sync visual pacing with @Audio1, transitioning from rain sound in Shot 1 to calm morning breeze in Shot 2.
Constraints: In Shot 2, preserve the exact packaging shape, colors, and front label layout from @Image2 with zero text morphing.
```

## 2.3. Mẫu Hybrid JSON – Create Video

```text
Generate a vertical marketing video strictly following this JSON specification:
{
  "task": "create_new_video",
  "format": {
    "duration": "10s",
    "aspect_ratio": "9:16",
    "shot_control": "single continuous shot, no scene cuts"
  },
  "references": {
    "@Image1": "Main character identity, facial features, hairstyle, and outfit.",
    "@Image2": "Exact agricultural product bottle to be held by the character.",
    "@Video1": "Reference for body posture, hand gesture timing, and subtle handheld camera motion.",
    "@Audio1": "Primary Vietnamese voice track for full lip-sync."
  },
  "timeline_action": {
    "0s_to_3s": "The character from @Image1 stands in a sunlit green durian orchard, looking directly at the camera while speaking and gesturing toward a tree branch.",
    "3s_to_10s": "The character raises the product bottle from @Image2 steadily to chest level so the front label catches the sunlight clearly, nodding confidently."
  },
  "camera_and_lighting": "Medium close-up, shallow depth of field, natural warm morning sunlight.",
  "constraints": [
    "Preserve exact bottle silhouette, cap color, and front label graphics from @Image2.",
    "Maintain 5 natural fingers gripping the side of the bottle without blocking the front label."
  ]
}
```

---

# PHẦN II: EDIT VIDEO (CHỈNH SỬA VIDEO / UGC / TEMPORAL EDIT)

Dùng khi bạn lấy **`@Video1` làm khung xương gốc (Base Canvas)** và yêu cầu AI can thiệp thay thế sản phẩm, đổi nhân vật, khớp khẩu hình (`@Audio1`) hoặc chỉ sửa một phân đoạn thời gian nhất định (`[Xs - Ys]`).

## 3.1. Công thức Tổng quát Edit Video

* **Chỉnh sửa toàn bộ thời lượng (`Full-Video Edit`):**
  ```text
  [1. Edit Command (REPLACE cái gì bằng @Image)] + [2. Scene & Motion Lock (PRESERVE cái gì từ @Video1)] + [3. Audio & Lip-Sync (SYNC với @Audio1)] + [4. Blending & Label Constraints]
  ```
* **Chỉnh sửa theo khoảng thời gian (`Temporal Edit [Xs - Ys]`):**
  ```text
  [1. Global Setup] + [2. Pre-Segment (0s -> Xs): LOCK] + [3. Target Segment (Xs -> Ys): EDIT] + [4. Post-Segment (Ys -> End): LOCK] + [5. Audio Continuity & Boundary Constraints]
  ```

---

## 3.2. Các Mẫu Text Prompt – Edit Toàn Video (UGC & Swap)

### Mẫu Edit 1: UGC Ghép/Thay Sản phẩm lên tay nhân vật + Lip-Sync (`@Video1` + `@Image1` + `@Audio1`)
* **Trường hợp A – Nhân vật trong `@Video1` ĐANG CẦM SẴN một chai/vật mẫu (Độ chân thật cao nhất):**
```text
Edit the uploaded video (@Video1) using the product image (@Image1) and voice audio (@Audio1) in a single continuous shot.
1. Base & Lip-Sync: Keep the exact person, outfit, background environment, lighting, and handheld camera movement from @Video1. Replace original audio with @Audio1 and accurately synchronize the person's lip movements, jaw motion, and speaking expressions to @Audio1.
2. Product Replacement: Seamlessly replace the object in the person's hand in @Video1 with the exact agricultural product from @Image1. Match the perspective, scale, and natural sunlight/shadows of @Video1 onto the product surface.
3. Constraints: Preserve the exact bottle shape, cap color, label layout, and logo from @Image1 without text distortion. Keep the person's fingers wrapping naturally around the side of the product without covering the front label.
```

* **Trường hợp B – Nhân vật trong `@Video1` TAY KHÔNG (Đưa sản phẩm vào tay):**
```text
Edit @Video1 by combining @Image1 and @Audio1 into a realistic 10-second UGC video.
1. Preserve Base: Keep the exact character identity, clothing, orchard background, and handheld camera movement from @Video1.
2. Product Insertion & Action: Have the character hold the agricultural product from @Image1 naturally at chest level, tilting the front label clearly toward the camera while gesturing with the other hand.
3. Audio & Lip-Sync: Replace audio with @Audio1. Synchronize the character's lip movements, smiling expression, and head nods precisely to @Audio1.
4. Constraints: Keep the product packaging and front label design from @Image1 sharp and unchanged. Ensure realistic 5-finger hand anatomy gripping the side of the bottle.
```

### Mẫu Edit 2: Thay Nhân vật trong Video bằng Nhân vật trong Ảnh + Lip-Sync (`@Video1` + `@Image1` + `@Audio1`)
* **Trường hợp A – Thay TOÀN BỘ Nhân vật (Đổi cả Mặt + Quần áo theo `@Image1`):**
```text
Edit the uploaded video (@Video1) using the character reference (@Image1) and voice audio (@Audio1).
1. Character Replacement: Replace the person in @Video1 with the exact character from @Image1, preserving facial identity, hairstyle, glasses, and outfit from @Image1.
2. Motion & Scene Preservation: Keep the exact body posture, hand gestures, background environment, lighting, and camera movement from @Video1 unchanged. If the person in @Video1 is holding a product, keep the product and hand grip intact.
3. Audio & Lip-Sync: Replace original audio with @Audio1 and synchronize the new character's lip movements, jaw motion, and facial expressions to match @Audio1.
4. Constraints: Match the natural sunlight, shadows, and color grading of @Video1 onto the character from @Image1 for a seamless blend with zero flickering.
```

* **Trường hợp B – Chỉ thay KHUÔN MẶT (Giữ nguyên áo kỹ sư, cơ thể và chai thuốc đang cầm trong `@Video1`):**
```text
Edit @Video1 by swapping only the character's face/head with @Image1 and syncing to @Audio1.
1. Identity Swap: Replace only the face and head of the person in @Video1 with the facial identity and hairstyle from @Image1.
2. Preserve Body & Product: Keep the original clothing, body, hands, held product in hand, background setting, and camera movement from @Video1 completely untouched.
3. Lip-Sync: Use @Audio1 as the voice track and synchronize the new face's lip movements and speaking expressions precisely to @Audio1.
4. Constraints: Blend skin tone, neck transition, and natural shadows smoothly. Keep the held product label sharp and untouched.
```

### Mẫu Edit 3: Thay cả Nhân vật (`@Image1`) + Thay luôn Sản phẩm trên tay (`@Image2`) + Lip-Sync (`@Audio1`)
```text
Edit the uploaded video (@Video1) using @Image1, @Image2, and @Audio1.
1. Dual Swap: Replace the person in @Video1 with the character from @Image1 (keeping face and outfit from @Image1), and replace the object in their hand with the exact agricultural product from @Image2.
2. Scene & Motion Lock: Keep the background environment, lighting, camera movement, and arm gestures from @Video1 unchanged.
3. Audio & Lip-Sync: Replace audio with @Audio1 and synchronize the character's lip movements and facial expressions precisely to @Audio1.
4. Constraints: Preserve the exact bottle shape and front label from @Image2 without distortion. Match the lighting of @Video1 onto both the character (@Image1) and product (@Image2).
```

---

## 3.3. Các Mẫu Text Prompt – Edit Theo Mốc Thời Gian (`[Xs - Ys]` Temporal Edit)

### Mẫu Temporal 1: In-Scene Edit tại `[3s - 6s]` (Nhân vật đưa sản phẩm lên ở đoạn giữa, không cắt cảnh)
```text
Perform a targeted in-scene edit on @Video1 between [3s and 6s] using @Image1 and @Audio1 in a single continuous shot.
1. Timeline Breakdown:
- [0s - 3s] (LOCK): Keep the original person, background, and speaking posture from @Video1 untouched, syncing lip movements to @Audio1.
- [3s - 6s] (TARGET EDIT): Keep the same person and background from @Video1, but have the person naturally raise and hold the agricultural product from @Image1 steadily at chest level toward the camera so the front label is clearly visible.
- [6s - 10s] (LOCK): The person lowers the product as the video transitions smoothly back to the original posture and gestures of @Video1.
2. Audio Continuity: Play @Audio1 continuously from [0s to 10s] and synchronize the character's lip movements throughout the entire video.
3. Constraints: Preserve the exact bottle shape, cap, and front label from @Image1 during [3s - 6s]. Ensure smooth arm movement at the 3.0s and 6.0s marks with no jump cuts.
```

### Mẫu Temporal 2: B-Roll Cutaway tại `[3s - 6s]` (Chèn cảnh cận sản phẩm/vết bệnh đè lên đoạn giữa)
```text
Edit @Video1 by inserting a B-roll cutaway shot between [3s and 6s] based on @Image1, synchronized to the continuous voice track in @Audio1.
1. Timeline Breakdown:
- [0s - 3s] (A-Roll Lock): Keep @Video1 untouched, synchronizing the character's lip movements to the first 3 seconds of @Audio1.
- [3s - 6s] (B-Roll Cutaway Edit): Cut cleanly at 3.0s to a macro close-up shot generated from @Image1 showing the product bottle in a sunlit green orchard, slow smooth push-in camera movement, water droplets glistening on the surface.
- [6s - 10s] (A-Roll Lock): Cut cleanly back at 6.0s to the original character in @Video1, resuming exact lip-sync to the remaining speech in @Audio1.
2. Audio Continuity: Keep @Audio1 playing uninterrupted from 0s to 10s (acting as synced dialogue during [0-3s] & [6-10s], and as voiceover during the [3-6s] B-roll).
3. Constraints: During [3s - 6s], preserve exact packaging, logo, and label text from @Image1. Keep character identity in [0-3s] and [6-10s] 100% identical to @Video1.
```

---

## 3.4. Mẫu Hybrid JSON – Edit Video (Full Edit & Temporal `[3s - 6s]`)

### JSON Edit A: Thay Nhân vật + Thay Sản phẩm + Lip-Sync Toàn Video
```text
Edit @Video1 strictly following this JSON specification:
{
  "task": "full_video_replacement_and_lipsync",
  "base_canvas": "@Video1",
  "preserve_from_base": [
    "background orchard environment and natural lighting",
    "original body posture, hand gesture timing, and handheld camera movement"
  ],
  "replacements": {
    "character_swap": {
      "source": "@Image1",
      "instruction": "Replace the person in @Video1 with the exact character from @Image1, keeping facial identity, hairstyle, and outfit from @Image1."
    },
    "product_swap": {
      "source": "@Image2",
      "instruction": "Replace the held object in @Video1 with the exact agricultural bottle from @Image2 at chest level."
    },
    "audio_lipsync": {
      "source": "@Audio1",
      "instruction": "Replace original audio with @Audio1 and synchronize the character's lip movements, jaw motion, and facial expressions."
    }
  },
  "constraints": [
    "Preserve exact bottle shape, cap color, and front label graphics from @Image2 without distortion.",
    "Match sunlight and color temperature of @Video1 onto @Image1 and @Image2."
  ]
}
```

### JSON Edit B: Chỉnh sửa Phân đoạn `[3s - 6s]` (`LOCK – EDIT – LOCK`)
```text
Perform a targeted time-window edit on @Video1 following this JSON timeline specification:
{
  "task": "temporal_segment_edit",
  "base_video": "@Video1",
  "continuous_audio": {
    "source": "@Audio1",
    "behavior": "Play uninterrupted from 0s to 10s with accurate lip-sync on all speaking frames."
  },
  "timeline": {
    "0s_to_3s": {
      "mode": "LOCK",
      "instruction": "Keep @Video1 completely untouched in character appearance, posture, and background, syncing lips to @Audio1."
    },
    "3s_to_6s": {
      "mode": "TARGET_EDIT",
      "reference_used": "@Image1",
      "instruction": "Keep the same character and background from @Video1, but have the character naturally raise the agricultural product from @Image1 to chest level so the front label catches the sunlight clearly."
    },
    "6s_to_10s": {
      "mode": "LOCK",
      "instruction": "The character smoothly lowers the product, returning seamlessly to the original posture and motion of @Video1."
    }
  },
  "constraints": [
    "Keep exact label design and bottle shape from @Image1 during [3s-6s].",
    "Ensure smooth arm motion transitions at the 3.0s and 6.0s boundaries with no frame jumping."
  ]
}
```

---

