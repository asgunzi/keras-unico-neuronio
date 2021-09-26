# keras-unico-neuronio
Classificador simples em Keras, com um único neurônio em uma única camada


Redes neurais do mundo moderno podem utilizar centenas de milhares, milhões de neurônios artificiais. Porém, o que dá para fazer com um único neurônio? Resposta: um classificador simples. Segue um exemplo.

Este é o mesmo exercício visto anteriormente, de criar uma reta para classificar o Resultado em função da Performance e Dificuldade:
![](https://miro.medium.com/max/1272/0*bJyEyiX6nt63OLj6)


Performance = [6.8, 7.9, 9.6, 9.6, 9.4, 7.9, 8.8, 7.9, 5.8, 7.8, 5.9, 6.7, 9.3, 7.9, 6.5, 7.8, 8.0, 6.3, 9.4, 7.4, 9.2, 9.5, 6.8, 5.5, 5.7, 6.2, 5.6, 6.6, 5.5, 5.5]

Dificuldade = [8.0, 6.5, 8.4, 5.4, 7.2, 8.5, 8.5, 9.3, 9.3, 8.3, 9.6, 9.1, 8.9, 7.0, 9.1, 8.1, 9.2, 9.1, 6.5, 9.8, 8.9, 5.4, 5.9, 5.6, 5.5, 6.6, 5.4, 7.0, 5.9, 5.4]

Resultado = [‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’, ‘Não Ok’]

No exercício anterior ( vide aqui), o classificador era simplesmente a reta x + y = 14.

Um neurônio artificial é comumente representado da forma abaixo. É exatamente igual a um classificador. Recebe valores de entrada, multiplica por pesos e soma uma constante.

É inspirado no neurônio do cérebro humano, onde os dendômetros recebem algum sinal de outros neurônios, e o axônio dispara uma composição dos sinais de entrada para os próximos elos do sistema.

![](https://ferramentasexcelvba.files.wordpress.com/2021/09/artificialneuron.png?w=473)

Vamos usar um único neurônio em uma única camada, para criar um classificador. Ferramenta: Keras, um pacote de AI que funciona sobre o TensorFlow, um pacote de computação eficiente do Google.

from keras.models import Sequential
from keras.layers import Dense
from tensorflow import keras
from tensorflow.keras import layers
import tensorflow


Declarando o modelo
model = keras.Sequential()


Adicionando uma camada com: um neurônio, dimensão do vetor de entrada = 2
model.add(Dense(1, input_dim=2, kernel_initializer=’uniform’, activation = ‘sigmoid’))


A seguir, criar uma função de otimização, a métrica a otimizar e manda rodar
opt = keras.optimizers.Adam(learning_rate=0.5)

model.compile(loss=’binary_crossentropy’, optimizer=opt, metrics=[‘accuracy’])

model.fit(X,y, epochs =100, batch_size = 10)


Resultado, convergiu com uma acurácia de 96,6%, é um bom modelo.


Epoch 100/100
3/3 [==============================] — 0s 3ms/step — loss: 0.1256 — accuracy: 0.9667


Via o comando “predict”, vamos predizer o resultado para combinações de entradas:

x_test = [(5,5), (3,8),(8,8), (7,5), (7,8), (6.8, 8)]


print(model.predict(x_test))

[[0.00640216]
[0.01692742]
[0.84710884]
[0.06093016]
[0.6358352 ]
[0.5808778 ]]


Nota: o forecast é uma função contínua entre 0 e 1. Para traduzir se passou ou não, vamos usar outra regra. Se o valor for maior que 0,5, podemos dizer ‘Ok’ , senão, ‘Não OK’.


Vamos dar uma olhada nos pesos do modelinho.


weights, biases = model.layers[0].get_weights()

print(weights)
[[1.1547703]
[1.0974979]]


print(biases)
[-16.306044]


Ou seja, esse modelo pega a primeira entrada, multiplica por 1.15, pega a segunda e multiplica por 1.09 e soma -16.3.


Isso dá muito próximo à reta x + y — 14 = 0, que já tínhamos encontrado.

Modelos mais complexos podem ter dezenas de camadas, centenas de neurônios por camada, função de ativação não-linear, camadas especiais (como convolução) e outros truques que possibilitam ferramentas de detecção de imagens, algoritmos de tradução e reconhecimento de padrões utilizados no mundo atual.


Exemplo: Arquitetura do Alexnet, uma das primeiras redes profundas. Cada retângulo é uma camada de neurônios.

![](https://ferramentasexcelvba.files.wordpress.com/2021/09/alexnet-architecture-includes-5-convolutional-layers-and-3-fullyconnected-layers.png)


Para quem quiser rodar, segue link do Colab:
https://colab.research.google.com/drive/1gURlAAKEWZ2rRbdTrWtnhThIE7tBDM1X?usp=sharing

Coloquei também no Github: https://github.com/asgunzi/keras-unico-neuronio
Veja também: https://medium.com/ideias-anal%C3%ADticas-avan%C3%A7adas
