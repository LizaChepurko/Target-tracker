# :satellite: Satellite Target Tracker 

A Python framework that computes a satellite’s circular orbit over Earth, generates customizable ground-track “target” points, and produces a dynamic Google Earth Tour complete with animated highlight circles, variable camera ‘watch’ radius, and automated freeze/resume logic, packaged as KML for visualization in Google Earth Pro.

---

## Screenshot (speed x1.8)


https://github.com/user-attachments/assets/8916909f-8696-48e9-b0c6-2cf88fb790ca


## 🚀 Features

- Compute a satellite’s Earth‐fixed ground track given:
  - Altitude (km)
  - Inclination (°)
  - Orbital period or derived from circular orbit
- Generate evenly‐spaced “target” points around the ground track.
- Draw a circle around each target on watch mode. The circle shrinks as you approach the target and expands as you move away.
- Create a Google Earth **Tour** that:
  - Flies along the orbit.
  - Tracks when approaches the target.
  - Freezes the camera (to save “fuel”) when outside a specified target radius.
  - Resumes tracking when entering a new target’s radius.
- Output:
  - `.kml` for preview
---

## 🛠️ How It Works and parameters

- Orbit Propagation: compute ground-track lat/lon from circular orbit model.
```bash
def eci_to_llh(θ):
    lat = np.arcsin(np.sin(inc_rad) * np.sin(θ))
    lon_deg = (np.rad2deg(θ) + 180) % 360 - 180
    return np.rad2deg(lat), lon_deg
```

- Target Generation: choose how many targets you want and the deviation via "lateral_km" distance from satellite orbit.
```bash
def generate_evenly_spaced_targets(track_latlon, n_points = 10,
                                   lateral_km = 0)
```

- Change the watch range with "range_km = 650"
- Target Highlight Circle: around each target, draw a circle whose radius (km) is computed as:
```bash
circle_radius = max(min_radius, scale_factor * distance_to_satellite)
```

- scale_factor determines how the circle expands proportionally to satellite–target distance
- min_radius ensures a baseline circle size even when distance is small

## 💡 Instructions and output file

You can use [output_example](https://github.com/LizaChepurko/Target-tracker/blob/main/output_example.kml) file.
1. Download `output_example`
2. Open "Google Earth Pro"
3. Click on "file"
4. Click on "open"
5. Open the downloaded file
6. Click on the camera icon under the "Orbit Tour" to start play the simulation
  



