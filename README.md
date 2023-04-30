
# Edição vídeo com moviepy
Este projeto consiste editar vídeo com python, utilizando moviepy.

Neste projeto foi realizado corte de vídeos, acrescimo de legenda, retirada de áudio, e inclusão de áudio.

Inclusão de Legenda
---
As etapas são:

1. Importa a biblioteca;

2. Crie um objeto VideoFileClip com o arquivo de vídeo;

3. Crie um objeto TextClip com a legenda que deseja adicionar;

4. Defina a posição da legenda no vídeo;

5. Adicione a legenda ao vídeo usando o método CompositeVideoClip;

6. Salve o novo vídeo com legenda.

---
_from moviepy.editor import *_

_video = VideoFileClip("nome_do_video.mp4")_

_legenda = TextClip("legenda aqui", fontsize=24, color='white')_

_legenda = legenda.set_position(('center','bottom'))_

_video_com_legenda = CompositeVideoClip([video, legenda])_

_video_com_legenda.write_videofile("nome_do_video_com_legenda.mp4")_

---
Outra maneira seria:

---
_from moviepy.editor import *_

_video = VideoFileClip("nome_do_video.mp4")_

_texto_legenda = "Este é um exemplo de legenda"_

_configuracoes_texto = {"fontsize": 24, "font": "Arial", "color": "white"}_

_legenda = TextClip(texto_legenda, **configuracoes_texto)_

_legenda_posicionada = legenda.set_pos(("center", "bottom")).set_duration(video.duration)_

_video_com_legenda = CompositeVideoClip([video, legenda_posicionada])_

_video_com_legenda.write_videofile("nome_do_video_com_legenda.mp4")

---

Caso seja necessário colocar a legenda em local especifico do video mudaria:

---
_inicio_legenda = 2 # em segundos_

_fim_legenda = 5 # em segundos_

_legenda_posicionada_1 = legenda.set_position(("center", "bottom")).set_start(inicio_legenda).set_end(fim_legenda)_

_legenda_posicionada_2 = legenda.set_position(("left", "top")).set_start(8).set_end(10)_

_video_com_legendas = CompositeVideoClip([video, legenda_posicionada_1, legenda_posicionada_2])_

---

Acelerar vídeo
---
Etapas:

1.  Importe o módulo necessário;

2. Crie um objeto VideoFileClip com o arquivo de vídeo;

3. Use o método speedx para acelerar o vídeo. O parâmetro x define o fator de aceleração. Por exemplo, se x=2, o vídeo será reproduzido duas vezes mais rápido. Se x=0.5, o vídeo será reproduzido duas vezes mais devagar;

4. Salve o novo vídeo acelerado;

---
_from moviepy.editor import *_

_video = VideoFileClip("nome_do_video.mp4")_

_video_acelerado = video.speedx(2)_

_video_acelerado.write_videofile("nome_do_video_acelerado.mp4")_


---
A aceleração afeta tanto o áudio quanto o vídeo do arquivo. Se você deseja acelerar apenas o vídeo e manter o áudio original, você pode usar o método without_audio() para remover o áudio do clip antes de aplicar o speedx(). Depois, você pode adicionar novamente o áudio original ao vídeo acelerado usando o método audio.fx(). Em seguida, você pode salvar o novo vídeo com áudio usando o método write_videofile(), como mostrado anteriormente.

---

_video_sem_audio = video.without_audio()_

_video_acelerado = video_sem_audio.speedx(2)_

_audio_original = video.audio_

_video_acelerado_com_audio = video_acelerado.set_audio(audio_original)_

---
 Para acelerar em direntes parte do videos dever temos:
 
 ---
 
 _video = VideoFileClip("nome_do_video.mp4")_
 
 _parte1 = video.subclip(0, 5) # os primeiros 5 segundos do vídeo_
 
_parte2 = video.subclip(5, 10).speedx(2) # a partir do segundo 5 até o segundo 10, acelerado em 2x_

_parte3 = video.subclip(10, 15).speedx(0.5) # a partir do segundo 10 até o segundo 15, desacelerado em 0.5x_

_parte4 = video.subclip(15, None) # a partir do segundo 15 até o final do vídeo_

_video_final = concatenate_videoclips([parte1, parte2, parte3, parte4])_

_video_final.write_videofile("nome_do_video_acelerado.mp4")_

---

Deve ser definido as partes do vídeo que você deseja acelerar em velocidades diferentes, usando o método subclip(). Neste exemplo, a primeira parte do vídeo é mantida na velocidade normal, a segunda parte é acelerada em 2x e a terceira parte é desacelerada em 0.5x. As partes do vídeo deve ser juntadas usando o método concatenate_videoclips(). E por fim deve ser salvo pelo metodo write_videofile().


 




