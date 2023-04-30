
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


