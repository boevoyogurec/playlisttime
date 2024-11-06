import random
from datetime import timedelta

playlist_c = (
"Happy Nation; 3.32",
"It's My Life; 3.59",
"Lady(Hear Me Tonight); 5.07",
"Fields Of Gold; 3.38",
"The Winner Takes It All; 4.54",
"Self Control; 4.06",
"I Shot The Sheriff; 4.57",
"Don't Give Up; 6.34",
"Relax, Take It Easy; 4.30",
"Dancing Queen; 3.36",
)

playlist_b = {
'Портофино': 3.32,
'Снег': 4.35,
'Попытка №5': 3.23,
'Тополиный Пух': 3.53,
'Если хочешь остаться': 4.48,
'Зеленоглазое такси': 5.52,
'Ты не верь слезам': 3.1,
'Nowhere to Run': 2.58,
'Салют, Вера': 4.44,
'Улетаю': 3.24,
'Опять метель': 3.37,
}

def parse_playlist(playlist):
    if isinstance(playlist, tuple):
        return [tuple(song.split("; ")) for song in playlist]
    elif isinstance(playlist, dict):
        return [(title, time) for title, time in playlist.items()]
    else:
        raise ValueError("Unsupported playlist type")

def get_duration(playlist, n):
    songs = parse_playlist(playlist)
    
    n = min(n, len(songs))
    
    selected_songs = random.sample(songs, n)
    
    total_duration = sum(float(time) for _, time in selected_songs)
    
    total_duration_timedelta = timedelta(minutes=int(total_duration), seconds=int((total_duration % 1) * 60))
    
    return total_duration_timedelta

total_time_c = get_duration(playlist_c, 3)
total_time_b = get_duration(playlist_b, 3)

print(f"Общее время звучания для playlist_c: {total_time_c}")
print(f"Общее время звучания для playlist_b: {total_time_b}")
