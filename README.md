# Guia para crear Prototipos de a partir de un juego preexistente

*Crear un prototipo a partir de un juego preexistente*
*Conocer algunas Interfaces útiles de Unity*
*Crea tu protafolio!*
**Pre requisitos:** Tener experiencia básica en Unity o haber tomado este curso [https://platzi.com/cursos/desarrollo-unity/](https://platzi.com/cursos/desarrollo-unity/) 
![enter image description here](https://lh3.googleusercontent.com/fDVU8_S9vdcJgwOuJVpfAHNIoOg354BxKVp98PaKYx51fXS6yEX8O25h_9s6eNjakKsTvk5hk0VT7eGTUSNkTMy6f_zyAtavKfE6tfOPflxeovz3J5qx9evKcPZyCgcgl9mp33gJuzQnjXC8hB5coBZENtiLDJHf03a6-PvObfArWRHgtpEAvY3Uf5pwM1oqE9OkmnxdHpLYvSSQSzGqsnfRRvle4Z4QBdEDKH0-Rhy19-dx6X5aqMRWOED2CXG0LslNsY9_x-SQitJTpMz16aLppZu1Hq1ThxvBGzuFwDbf4f77P7hwWLhYuU2lbNWHSrQokmbYgP5L4ivN1jSdNHZkwqt9-7dIh7kfiSG1W0ZhaMyB-jEV4AnJEE0yfjDdpBa1POIaulbiqih7_XSbDlTZM-ch9jvdrEp8zg4GGva1jXqVKC5l9I5EpYJ0-mI3Y09AhXwFrcIYrN0gQR51VpC52yyedBFJHKkmnxo3Spm1-u07HuNIU-isK8s2VkI60ltuCpfRGb1tszWzwLS8lucAlXQEBoo4InsvIAHK45Z3x_CX1GTDUj-_X-Nh7Q8hNBai1rPp72QS6BciebufJrif5TrRQIpTq2XdCP5W8YTfUIkybrOwCFgz757y903osGxsNMlvqfRlPXECGQMMI7_oX-6rtabszc12BwY08eL3IXW0YuJ19Zxi0t5IXmUW17FeUmHKb2hvxLpn9MGMxHeWz4cOosvFjcU08NrXa3kVUqI=w372-h667-no)
En este tutorial vamos a crear un prototipo a partir de un juego publicado en IOS. Este prototipo será desarrollado con la versión LTS de Unity 2018.4.12f1, pero no hay problema si usas una versión avanzada. 

Veamos este vídeo
[https://drive.google.com/drive](https://drive.google.com/drive/folders/1tI-TKiZB2RhK8RejxKIn9i39LYd6mPTo?usp=sharing)


## Break down
 Si quieres hacer un prototipo basado en un juego existente, debes analizar paso a paso sus mecánicas. Por ello, te recomiendo que te hagas las siguientes preguntas: 
 - ¿Cómo crees que funciona su mecánica principal? 
 - ¿Cómo crees que funcionan los controles? 
 - ¿Como lo harías tú?

 Como futuro desarrollador de videojuegos, debes comenzar a analizar tus experiencias como jugador. Es muy útil hacer este pequeño ejercicio cada vez que te sientas interesado por algún juego. Esto te ayudará a crear hábitos de un verdadero desarrollador  de videojuegos.

 Ahora que haz analizado estas preguntas, debes pensar en como dividir las mecánicas en pequeños trozos que sean sencillos de implementar y rápidos de testear. 

> En este tutorial nos centraremos en el apartado de mecánicas y cómo implementarlas en Unity.

Según mi criterio, podemos dividir la mecánica principal de la siguiente manera:
 - El personaje principal sube gracias al trampolín.
 - Baja por fuerza de la gravedad.
 - Cuando gira, el usuario puede controlar el giro a la perfección. Es decir, que puede cambiar de dirección con facilidad. 
 - Si el personaje esta girando, igualmente avanza hacia delante.
 - El personaje puede avanzar sin la necesidad de girar.
 Por lo tanto podemos graficar la mecánica con este diagrama de flujo:
```mermaid
graph TB
A(FixedUpdate)
B[Avanzar]
C[Rotar]

A--> D{Esta tocando la pantalla?}
D-->|No|A
D-->|Si|B
B-->E{Deslizo el dedo?}
E-->|No|A
E-->|Si|C
C-->A
```
 Recuerda que FixedUpdate es una función que se llama en cada Frame, luego de realizar el Update. Normalmente esta función se utiliza para hacer movimientos que tienen que ver con cálculos de físicas dentro del juego. En este caso,  lo vamos a usar para mover y rotar a nuestro jugador, mientras se ve afectado por la fuerza de la gravedad.
 
### Montar la Escena
Abre Unity y crea un nuevo proyecto 3D. No necesitas ningún extra *asset packages*, ni tampoco agregar analíticas. Si aun no haz personalizado tu editor, se abrirá el layout por Default.
Luego de tener Unity abierto, debes buscar la opción de *File > Build Settings* y seleccionar *Android o IOS*.

Utilizare un Layout diferente, Tall, ya que será más cómodo trabajar este proyecto de esta forma. Lo puedes seleccionar en la parte superior derecha. 

![enter image description here](https://lh3.googleusercontent.com/BdBpHG3zztU4Gzc3oY0SVAR-5svmKBXspWw2ifD1qPNz4gJsZu4lQW5H1dS7Zdqs5fn0r3WHLFb9CBWH8LwtEV0WCcZ4e_2Y9ZmRVhINOfB8Y-UrYhOwYMiMjAFFB4rdlzbsCaGTHu5l0qGFFhrcndeKod47tz6Y0gy0GoF7W77ACCPQgV3biIw-E7HNEH4U0I3v2POtmw2MZrOErpQO__9vJfMtLTvWhPuqg6-7eQAlHOVjbWyUTPr2MIRYyb1WNa5iws7ysE3kWGY15of0FPlFqbWwCUNpoQepq-p11gWaYxSb6nqys_YHCjmsdWFpXL_xR00zXhQw_EakpYqGuDeRHdYE9Qyl9rT0I6WmYTbGvBbQuUsxzBH8q0Ic6BkDTg19Q54ZUDRkSg3HiyeCMBFU3CQp9zYLRhwbT0jK5IaH2Xqq8IGXOX7QEQCjgZhuq50lDPvL1wCag8pVGKym1yev9SCaNU0pbpgPY4LXoX5XmvOHVALrJnM78qzaeg55sc4DQB9nIDzgJ7iJVNUIRsY_EoxokRPsN_kDctXtxsg36vr7MmUSibN2n_41wR5k3wTjEcAaNcbOh8Z9NUVFILTMS7NP9z6Yp9_khVO70feV3Od7tVrO8FMEoLRKTbVSNHwSMTq6C9Ap8FVZJARfVx2otSvrGKeHJsC1f8i3EErOzsC-1TlFFW2-JsBYfMSks0MbLiEBQspY3oBV1iQ544aRCH-aAGY1RPJ4vzxpT9-Zgyg=w630-h614-no) 
![enter image description here](https://lh3.googleusercontent.com/-VusEWahVe6JMcMHR-qf7xsqcSVTBJ1P-L7obIMivRV7KRYNLkAEjpFFU8M4h7pybYFwoN9C-mp22ZmuMxOVkWry0p1yX4PyrA8TCbLVt-cZndESqD-Q9RuEW5Ozz0hv45F7cNuvuxyMO19droIDCMFLnlpXX6zJx8siO74Ij9PsSqzHNuL69hZQXhHLlEhimc5qffQkKvZO4uXCZCLQ7imsdLGEA9Kn9BHYNoymp1tvSrtIJnIot62-KcehaK4NMykEKdtLZ0VdSAi0wAGi1VQyCGPDAe4BMDBhQSsl6QUyp82HSKSiv5PvaL8aD2xqbt6p-BAtkyDVtTAkOGEOBaL1PTt6IHuOhTftXXvlNdUFN5bHqUPw6y66DD4aWVj_AlGT4fNr4tCsJA0hd_sEenaSmQGhxAHXOc9m0MY1BcQNEcIFQbLBK8CEe9SeiVcwEXkePgsxgjB0CCpneEzw1UONO3ywPB0aGujNhRl-n7n6WtldtKSbYw9nnsnwcF93lH1T7CRh5-YLlO-_wgNuCdaqehl_ZaZd5groxErLp_801Sq0ip758ZFtCVNsHedeU1UeDxoqBRk0ack-I4RxA7GTz5NxdCN6FMZdN_d_EbeQl7_jaaggFG1SXKvXkszcxPZ9WBr0qwkh24dGCIP41RWicP7GEBvUPcnydmQO2nPhDnS3YZlc8eySxNYHIOunVXZBWWd2Fx3Sdx3YCaLsCclcVpXofCl0eeTO1YXdUNZ7it8=w1287-h667-no)
Ahora que ya tenemos nuestro espacio de trabajo listo, continuaremos creando nuestro jugador, que en este caso será un cubo. Para esto presionamos click derecho sobre la ventana de jerarquía(hierarchy ) y se desplegara un menú escogeremos *create>3D Object > Cube* Luego, cambiaremos su nombre a Player.
Tenemos que encontrar la manera que nuestra cámara siga a nuestro jugador. Por ahora, podemos que la cámara sea hijo de Player, para hacerlo solo debes arrastrarla encima y se colocara dentro de nuestro jugador en la ventana de jerarquía. Esto  permitirá la cámara siempre siga al jugador,que en este caso sera su padre.
![enter image description here](https://lh3.googleusercontent.com/zdB5AEvuQ2_sDb9WiR8oEKTxjhcAkaoHz5JR-uVjvQFVTSvJ3HukBB8oejWOws4ilUNuDZxrFoIjHd2yI5na3NffK-rMjaji0MyXz1Sv9BlxunFaeoSDCQi3jo4l1TU6CAJBnEBZXhG-Rdd9v_FadEVFu5DTsWPgu3Bgi7a5FfLMl-9UJqxNNAJzA2h4yO7_HjIDRoQMnH1jEUb26KHRLf7yXQ9kF1O-9LgYaTBPsNUzOiS0pi1e2G22jAtw9EXcmV5fASeGkgcRENhSzKC_YSn--syfh0YK7xohCYWtmNcAsveT4OmUZo17GgdoRIv9bjOzOB6l4ZpnTBabKRqIP_QdSzvB5IHJ4s8w17gyFF_vzPhYnD38Lxg5J2Krm-tnGdvP2o-HT5C0pEZf0qCzKR_kKFgqali0TjzgnzHkSqNPr1SAc84jRwk7ndzd3jf3zC5992p4xAQH303AElbe-SYgO7aHQBAp8MPdrd-bQRuCZMNBOXB6dziMPL-FfK-CRi21qisszQ1yi7FmR6T0geiWpZpzmwpsdqztMcf_eNk2kj3gKOjiVxNt2PuuN3jedM5E180g7pAILPSPDvvMQvzi_Azx_yTv7sBzQxaI_MiJLb-EVlBGYhHMiSCIuh733_a629kr0T8Kxu8_GUziMih66D26x3ILJfliCnEmxiTOPw4UbfQqfqoSHSLN1peOB8U64khKkT254McDmngg6tnYnKDCdjOORuzqDCFEoO3n3rI=w380-h53-no)
Ahora necesitamos crearle una apariencia a nuestro personaje. Por ahora, crearemos un material llamado *Player_Mat* en la ventana de proyecto, esto lo haremos haciendo click derecho en la misma ventana, seleccionas *Create>Material* y se lo añades arrastrando el material a la jerarquía donde esta el cubo con nombre Player. 

![enter image description here](https://lh3.googleusercontent.com/TS9i11i6S3gC064QBwzJrkZ7ts3ska0aO_JvCnGfHzD4sG1YhHax0rMe01EEoseHPJp-nLPkIzFs7nFr2gt2lRZSjhz3VQCfnCAWPfFOyMkefq8HPN97uPXKZD96vPme2tm1VFeOUbW9qLRSWjaAciEswelg00fo9O4XIEB6-DegfOBp-ZDWwgDM1N0IoG8TcF9clWJNfRcx14VBbOVJz8BwBg0al6-y5HCfnw1wugGwed7_tNg797-HggmAO1vbXHKlBQaD24KcvvlIJkrbrklMkSLBUpgiqrJVoY9c4h4yTu3J9MYp7CxbD8vEc0S1KS-Dyao3U9kxBb7WPHnIpyyGXoF-RerPISCGYg_HBl9yt93AaISozBxPLIdGrebJ_HMkTHTjjWxCutFsDF0kG4HyXPo0FUa9AS904QB8iqg6CdwvJ8IyfwzIxqERKKmGNJyg-JmvXcufRo9QX4Md15l2eC9xeU-AUWHRcYB09Y1Tw_AQKnL6bUVOcIVCc8DkxONaYKkG52yx4pUfV2ClhDwSONsIIdV0YqsrQ3JYc-5bIbggEABSv1iMfmK0UmoADH5E7ifYFiyxsSyek5HWEWWs970o4Xpi6co04HiAUfJ-g4JVI3pFGip8Ab3_JP_ulajq-wWHR6gMWWC0egzy2NRVgubOViqHbP9Uz58EVjgavT_UoHUtsYD2bKo5FER9Ky_JKvCZqe-ZANT85BzgddDSpFp7GABU3QjpFIuGWWjpfts=w374-h69-no)
 Para mi, esta configuración de angulo y posición funciona bien para la composición de nuestra escena pero puede que mientras vayamos jugando estos valores cambien para tener un mejor resultado.
![enter image description here](https://lh3.googleusercontent.com/dDQEgeD4200KlI6sVHdWLHECfDIKxrR1uQstAyXKBLzJZpSdLmciKooR4vMXkE6qbk5b1g_WLS4b7xn37EuKfKP9w1hPITCqis-KQaa1FSGwNq_t3t4b2LsBT_t260sSiV2ysPPV412w0aeoWyrKth05_a0JYZ7IH53vhl6LkDbOBKDWQn-NMdEejOA-sgzZu6a33GEhLKj899yRMO2IKVqCOyfjxosDU3F9w71kzYUDhe4-K5ihjRxrJHPE24Ey2fcGjAuVHhkyT4NVcgdnAL2UQCZ2tg53VqarQuOuasp8xe4QdBPNCUAKdu2GPW3oP0au2fRq5IaMEM6QMoS7NiSsgmTnpEIV5aTfWQmhSsDvgj11CGa8n6udVS4u6Fh7C_tQASf7c1xAJB2YhOTqsfcFstdm2vpE03-mVNvVMAhjFJwjQVNV7nXhY8Hb6ZsmizUsWdlBKyjXBpa_SKYxA8FfW_SomMCS0ldX9xPKUUkn_qoakZIlPjDPW236f2Wmm5uAgZ5OpELiOXugkIQNK41v-NNsHv90XPyVheDwgkdjbO62_oUFQzf6ceqjNsFvphctnbu--ay8FLD_MWKNnOp_qMe5nMMq7KUWEZ53zIimT1VHBXEgLx0zD856Jchwu3GIkqmkg4Hs_E8ZIIkrhITnohhlPz3-A8887FFtkrmUumTgSryeS6-eEZH2yWkQ062XYY0M7GFV6ZQK7HozCQ2LlicmVWaI3VaZ7BX6zybOX40=w459-h424-no)
Ahora crearemos nuestro objeto para rebotar. Para eso, creamos un Cube seleccionando *GameObject>Create>3DObject>Cube* al cual nombraremos  *Trampoline*. Te sugiero coloques en el Transform  los valores que aparecen en la imagen para que hacerlo lo mas similar a una plataforma. Mas adelante podremos cambiar el modelo. Cabe destacar que añadí un material de color Celeste que tiene buen contraste con nuestro color de fondo.
![enter image description here](https://lh3.googleusercontent.com/KXEaFaq9c2_88meZyD6Znt7lcQii6_EoAHuOjm51zk69dWcLQrQyGg3krTW-51ZfL8_ToFbibcGDGhG67MS3hu3abHmc7qSfkg0lC5Qqz4hFrFdYPc_GqCdKqA1TKuxymLJUmmarURk90haaBvvpeXv07BTesmh-dY-hW5Mc7wUK0b0ZiyRPxzoWfkX8RvCVZ91nTB9cexPn95r8ENFaGrwAzS5McXoFhAqkEzfZkTH-2nI8gbpx7qZlecibNwbDWfUltfcKf5eWMLY-J0d5UIo-gHsx1wkrK3tp7pf7szFnUb7gxwESLzzic5GGgdLrAGefSlI-nn1QOm7expJ8kPsesWtWw-QpogTispPInmUJ5rcmO60pNFyZZ51fXYbxLK99_jmrliAsEOqQVum51G6imMzZAPRuYbMOo076X2KEjBk8saoItyRB35-GoT1hXJ-s8TTRzMOTdj8uMJYS6Cz3BEBHXJEgHx5Mt5yxDAOlEpMlX0An_iC2ko2A8zD6e7bohjf2mcMtNka8Ak2_-Ke-f7LnUHxMrDfkGixrrNrjj8WvSdtr0DCBODGj1hzEZd2IkfPXXFwG40C6trhPtRFpCrYkP0phxVMrxzMiPNkutuhhmZAv7mALzn6Phv3aIyYVQh-UZXSbxc13Fo9Un0QeWD7Vav0CKM98jEf6zTE3cVyMe0zhnmxs674ATS-iTrYqxE_YxPBP5ZRTqX6VfmpmV4zNKJqAAcPSnmt3t3acH24=w449-h528-no)
En el Player añadimos un componente de *Rigidbody*. Esto lo hacemos para que soporte físicas y colisiones.
![enter image description here](https://lh3.googleusercontent.com/1hPCQp-GgXMW_cID0V9kwGtvCnwOlveBztF-LB8Vu7qvMpbsGCI6OJ7gmw90OUysKmxDzgvtD7KDxTsZ35Bprzw5lSPaAvNOKoCFFshY-td4RjFc6rqmCTOdE7a5KHmqzeQiW1U7zYq94NWsuP7FAINGYLBRVncQ0lpHDJ8E0u7UTjFBvM8qHMxFDIcbg-5bnWCAgK-LH1_7kFP27CNeUeq5M8QUtw6fSgYQFXIMCT_xJehLScP70_toQoE-_jo2GohwZSdM4r5RaPBUkAA8xe_51xdHH_AM2BJh9md1GQBkl7804vRWCic0Bac-3cMs2AOzBLXgwnoA_lANjvV3MJxOkoElgsY2oatiLYTxzEz_XAyjyfr2ybUbgBCk-0Juslm2MDrZmZiZS2hHn4EF95LMDi5zwfR7HGhWEwPC9L3Qj1Zw7JglFwYC9PSjWFE_GIVVoEomDQ3bSIJ6w_BO0fu2lkjFPB91eg6xbgpSRowCebZ_OKltw9UUu2PnlVNX3BkmXVE6m5en4mtRHaEMWqua0NJJ1mwGKx4RI2bHSqjy879yOzxytwQChKax9GU1uTxVHjEvfEyWZWlsCZ7f9NDH2n5VM7kY6OtkqzLCXOrDkXjX4VK3rPp6jc4plPHyp0ohEgcEjm_1VhxJmp3g_59MbWmvlCmIm8WZ8uqxe2PptlhL66WXkalyaVj681ba0PXjj3QoOTKlPXNkwU7yoMyeg2eBYT3S-5DVK92UDqkkJ3U=w460-h277-no)
Ahora vamos a nuestra ventana de proyecto y en nuestra carpeta de materiales le damos click izquierdo *Create>Physict Material* . Ese material se lo asignaremos a nuestro box collider del trampolín. 
![enter image description here](https://lh3.googleusercontent.com/vTKpX9txiyC6CaYS7g8gmedz0bDSYoKlCGmfLksl7QiGDB5ZD0Rlu2DOfhsyyoHnbauqhsRzKS37mGoS3J8r4kNZ4v8ZOJgiQGs5w0w9pTgFEkosN710B1PIFIFFeGjIV-3NcoHZnzG_auYip90WLaCjvpiDV0sxZkJ0_1PvY-D7mDI1CkLVM8vD3ae10Fo3-0RzjCPiB0JiNcnifBMo1u1l1EArWteb8WEHRDu0tCbMt_VjiKTZH8PJuOKiyqpnLaw9HqqRWNi4-pvgGMmptG7jdVxORu8WgLVfImH-kFLGvv2yPjOXQDZvIlXBlkeGPuIlEX5jk7tjzU6G2J7pChWicHj6k6ri4DKVQVl07MIUCxesAojMQMRhDZme5w5z0HF2EZW-2O8PY07oBSVjXishd95mpN74sbMFpMySmvE6BTk_ky4vdeGk_b-5sznZ1Wa12rASyp8N1JclJmuYOc0o-uDdpXEQAp8LNirKXzTgQ-8l3x1u5wTdPOxw9THFWU4Vi1BqjkQDV-OSa_aTMxpC0nBQhWwsM3UlezED5LvPzyUssWZon33EZNjvnPuAfhUJulahVc41a_lZmKCdrGp6nWLgSDQvMrRAT2en4p9g-OczR_RiwXMCvN3BadYPFV5yO8gwjEIMOfswVI5hhlf4MXYHHFNA31W2zg1xGw_vf9AY-Ak2cBWXn0jbLOHLG-HNkTGoB6kAiFYA-srKUGlYSipxfIZ29Wsh9foTLWZwhdw=w461-h133-no)
Esto para que este objeto pueda tener propiedades físicas. Los valores que debes darle son lo siguientes: 
![enter image description here](https://lh3.googleusercontent.com/MSdaO9j_6u1yEX8gltmqiI6hbsZJfTjufNNpJwNpCQuhy6-If3wy9md1Xc6IETu8Ia_zXbrTr2RVa5aIApeZcZpQeCQCJNqQ3pc2OqzaLRXqBZpW5WB-OKDBZtxhXjjTeJqTnpbbKIVVvGWSnb4TZ7LvIx5IrmLv5LfQegvkNV1RldG0j9Kg0yZad71IlXxzeEtT-dG73u3Zr0XLpXq9VrkVKJ_OU7pUiHgoHK33vDva6_i0i6hvoKiNYBxVRUxVk7Jtzk3W86jKyEy0rBaDh7XT53MCurdhpsqp2cSfDwydbtZlBWQdNuJ36GE3y31czh1qbfvmmTMtdMMvDhMQrDj4vO_7WrGictMqtfjATl_xE4flNn4sDmxxRmhm-fSrCnud2Wzdj6DHHZIn7thZ3c3ssloKft7388DNzBbM_o9VzwYQo5yS6JW83jLHSL0cPkhbB1oosNDOnzgtHKM53gT7Ht0oPCF8QOmYe6fJcry0HlMtDKLu98HTFc37HsDAJFznxnnuoXIXEm5s4Q71644S5zPY6QwklAabFr34RmXrY3d0HuRyL9Jvp2IKvWbqE-dA6YQVNkwZOtZ0-UQbssa5CqOoUTaCM-ehhSX1xCJAHSb3RYTvQq1XgrDKDtZsws0pPpBWcNhBg3S5V8eQLJQbDuplEFTqo2mlzonMs7bCngYJWmBeOWuVWZCTl1aX8aaSuUmTbW8HQtHNWxWzGbVtTpeLmUnkpOVYajkjMzhHTlQ=w456-h146-no) 
Es hora de probar que tal esta quedando el salto. Dale Play a Unity y mira como el cubo rebota. 
![enter image description here](https://lh3.googleusercontent.com/-Wh3McsxfEsgKfn6mUhLJ5r2FTD3Yl6yfqQ7g8MC-g4qnccKMc8rdvDQQXJB_T1vydWIEUVMomVT5mFXw1VlGtdEA2kv_HK2OkFoHYpBosWP0nV02ObmYBQ6H7qRI0FBJ4Dtm3rbtcU8MUvpq6mx2m27OhlUxmVZYsZqgEWMU4b-Zrj4Svjs_hItZxdqs8uJTvn0I883oSaT0kz2jkrNM2PFXyxdFu45aspOhMmHhKcjmbIDX4rBMhd_O-ycCqxkMXX7W4CKxyapJ-kH62NZwKGgcLQtPqTKyFINDlIXBG3DrRd1GmqHWP84ggTW_Lq_QqbKgIFmAcKMezCKo8zO3AlSQ5E_0KZvTHzVO0_bonnYeLm2xY0WiwRL23tW3t58XdUmKB1Qs4kTRX-Ip8rXvMYr92-WxLFekAcSvAEJCwvaeZZBt2SZTQj2xXn4-e15bwjy36bJTulcoO73wgr3itUEsfRleSee8rK1zZtwN5INUp_ZSEZ95oG7xpLSnttEPqQ7LgvcbQSLyVi-iNPW0EwhXIMTKJhD_ho_OrzugSh0I2a8xUnvFkESQ0NF5nhtEKAxsYt0A4VjP_wQQA0LdS3LhzUm1Hs746kzXS3r_Me2jCRWJj7oow0sEqPq8Ol4XbjAffAFuKFbyLXEd3a_QitT8L-eyhHKGvpPQxNFUTVcPqsJT5P47QUp0xnGE80sPMiqZg5OqGSRmLTmXZPu4YjSYs8NwrpRWLJX9Tg5JwUqA04=w374-h667-no)
Después de esta prueba, si te quedas un tiempo observando el comportamiento del trampolín, notarás que el salto siempre varia de altura e incluso no es consistente y por lo tanto no es tan fácil de predecir. La mejor solución para este caso es agregar este comportamiento por código, en la siguiente sección veremos como lograrlo.
### ¡Saltemos hacia el código!
Lo primero que debemos hacer es crear  un script con el nombre de Trampoline  y lo añadimos nuestro objeto con el mismo nombre. Escribiremos el código en ingles, porque es una buena practica hacerlo de esta manera. 
![enter image description here](https://lh3.googleusercontent.com/dDDiQEl72xeeTU7Ep1uvWV7mwjzfJKwY18w8-X0PLJK03W2h6j0udl1n9YzbZ2OcToA-xGfTkV_HI16AZuHvHvfBsjlZ-RrYh-Md_Cd3j4DdfsQULMqFYK9usNZOSxzx8s9qPW1wAjLilLm-uICrSJcNwfxy8aS_Xk1mp8rhOgEPrC6mSM9TQ_fXGZEg5a7Pzb-IXnJRbVzsXvBOALT5vrA2IUhXEB2oIeoj68650UVwf6vvNaNWcdj5FtqqFR31Tr3TOua1wDAWWntfUi7X6qd429nZyyh1Ka6euldCVZ4Pjox5gSmlPy164alRYNQ-eLY_7j1y1E6in9iygLPWVrU020xRdfHDUEaJm3O6SMfVjaYyWz7F0O4iu-qjWkXkycfdNuryWi8FjsJWhucS1e8XMLyeX-WrqnszLo8s5CMDdAD4TmJ4dqNrOOIvIVYRIP4PmrtT4m3irKDfZ114oboc9tl7Sd5nwlQLSZMgtbs5EaWt45CM5cKddJdxM6-i4Je1GJwpf3PFrMu8NRDaTy-E91N3Nmi_PAh9smJBtNxCUUOrdK_HlVfgp6bfZVdpwJnJJ1wOeMH9k-3JP0f82j4fQnTTmKWizLEBSMyoHArWxsMr1blt6Bd1MeroDJtgZTuRBJpQzcDbCSynxAgzzFjx0Pl4W2n8hCrzcIiygmRE-nMbC6P_B0h_p1DZ3Tc2zd9Mr8KvG732RY7u5VNaZejTPgVXxmKMJaR8D6KN-fQkYww=w460-h167-no)

    



```csharp
using  UnityEngine;
public  class  Trampoline : MonoBehaviour {

//Declaramos esta variable para controlar la fuerza del salto.
[SerializeField] 
private  float jumpForce =  300f;

private  void  OnCollisionEnter(Collision other)
	{
		//verificamos si el objeto que colisiona tengaun Rigidbody
	if (other.rigidbody !=  null) {
		//Aplicamos una fuerza para arriba "(0,1,0)" con Vector3.up
		// y lo multiplicamos por nuestra variable jumpForce que declaramos anteriormente. 
		other.rigidbody.AddForce(Vector3.up * jumpForce, ForceMode.Force); 
		}
	}
}
```
Luego iremos al *Rigidbody* de nuestro jugador y en los Constraints chequearemos las rotaciones. Esto con el objetivo de que nuestro personaje no tenga comportamientos extraños al saltar. Estas rotaciones solo se congelaran en el calculo de físicas, es decir que no tendrán comportamientos de rotación que tengan que ver con las físicas. Si las modificamos por código, podremos seguir cambiándolas. 
![enter image description here](https://lh3.googleusercontent.com/F0MfNXwsaL1LSGq7Ums8WfvX6txBrEekTapLwBdsVsYyyL7b6EWsKLC51KqWDGd3NOfazbUQE4HhR78xm7dJdQ3bNVyNP9ZS6r-Jy0DYq1gN8_Y46q9Yb6VSrZ0eQRDwz2lCKd0uhBB0jdIjU5fOlnk4HCk9-X-qZZEZeblI7z2xHMIis4LfEC5DiQZYLgs-RUjz6nVUK-MnME_-vwUqQIAGH_i4BkPU1qUpqXGMjGnRnDNDbyd8Q0tqyUyFjLW2yqgQ2NqgumhYs6wqrkriFUhMbX-xaTlgCZEGPbRze7m7qzXn7C_wDTMG4c5d2cgH8ErP7r11opIstPK3ZAPfK2VVi20lB-q62Xpqdm1Y6cWyJNMv1hjW2x8PEqwVcUy3_T8OOzhIV0PrxZhRt6f1qiap_77ODS0tpCJYlBWc5cLvhrpcYcEkAQCvmi9BFn3ERpVps57tYc0Az6Ks06xMpEbMI0brWnYlsipgjrV7Ka3FTf5ZM_9yFztpI_nWAURajx09UsTNclB5Jt53bjZ-6KppY5BioMycym0MIcyHAnSS_okUSGaQjUTRI_fFM85bEcQPlL135jkxKMut2WenlEQAWZd8lbCSLZCHsI4DqkpWevXRr5DAga9yMWpUQwwf8X5rHYdmhDjS9hZ7pVTMBEM5N1UtV4hfwZIfwJw9lvDGO2XP0O75fH6nBet0HNLSaLws5TWRtUthsLVm78HC7mVsScnIwtQKm94mE0YzYT-kO3o=w458-h237-no)
Probemos el salto dándole Play. El valor que le añadí al JumpForce fue de 450 porque fue el que mejor se adapta a lo que estamos buscando. No tengas miedo de modificar los valores, de todos modos estos pueden cambiar mientras vamos avanzando en el desarrollo.
![enter image description here](https://lh3.googleusercontent.com/i7aM-gf4hW4wgdmsT7BEF8jQFD9wik9Elxgf8RFX2KXHlBtjxecbqkrSXxtkfuijm-1_jOS-lGhxJDNiYjF1Zhc2o4lOHJlMyhCh8BjW41q9igJMBFYpJTMq6jaK2TrWmNTQ-Rq_UtrLRlyBkVeu-74wVRIm2K4HAIep8k2dNxFz81iMxInJLerFZulrx1jEJudh0SPh9kZ4WXY4JUAk2fC9VtMXGut4xawXAim-OdP8G-Lcpc5uyTKMUnpc9A2pVS7gYhCffZEujQPWjf4QCbqH8Zkkvy-9l1nvDbmSO7yz1GATD8GKpCnq29uUKIovfZ5vC7dWlchX40ttsuQQKHlbtCxoZO7_HOAgsS3y-FEeHjac7rMfq43YAoBsids0obvOXA2_ZkEn3mGIB94df9FaAy83OaRONXD25eDA3CAzXuIdgLHggimQCOXpSKebtI3a_kNESD9UMykuWmkEZ1_K284_nJJOo4zV8Tb8OpfAf9NrWwbcbMwgii4GqiCLnTvKH4GG7R5NQXd_i2A9pWYocL2_xQN0aBE1etU53TH07uW-fKRe_Mi5UC6QkXEAF_nt5aTut-SydCLfWPKdlZ32814d8-Li26jo4M4eG_X0zu4rNFDJ8EQQqHrMX5w1a6V4bWlZ0blnNTvZRPsP9cD3iE74S5FG1YFp8343ssJOfUkaRYiLSVU7Jb8XYhsYcL4y30p5MYLQxaV2t6NkM_Izt1gwCAkyLpMuL-kH2I4SkIo=w461-h175-no)
Luego de esto tenemos que crear nuestro Prefabs para poder usar nuestros Game Objects mas rápidamente y crear un nivel. Para hacer esto arrastramos nuestro trampolín desde la jerarquía, hasta la pestaña de proyecto. Luego veremos que las letras del nombre en la jerarquía tomarán un color azul, esto nos indicará que es un Prefab. Recomiendo que cuando vayamos a cambiar algún valor del Prefab, lo hagamos directamente desde el editor de Prefabs de Unity, el cual podemos encontrar al darle doble click al objeto o a la flecha que aparece a su lado en la jerarquía.

Ya que tenemos nuestro Prefab creado, hagamos un nivel para probarlo.
![enter image description here](https://lh3.googleusercontent.com/hkU0Tkzpk28xFAbtHghk2bOykqV22VK9jWtouCiCHsOvLBauoWpOzgPJd1haCVkMnDqT70DNU-hUqBhvHxU4LS97XzqvkaCuGS69DqQr-bs5srdIY8IBPdhM7I0yUTYR_JwmnFIUXH5aK1wG3xmUHXIoqdoXIU8wRormxHoRA0LfQkwUM70foqcHK4E8A12rcLdl7FoEOZ_ONlBa5FH0Ug-XG4T3vOMS2U1dYrug2i2alY0z0-L8zfmI_1pckaUiiavq5PpjUKFr_wUccvFexczutO3oBzEuht4dGyO7hG6relNShzdqfH58R1QABuM9Qjg_BzC_q3hV0tMl-qtyl3dG8Cn2mYeCADXK1-vsEEUQh9BxaSaesZYWWWdQv9SW4OJFu4_8P5zuMD__QOafXZCZ8qKIdg41ilJ8wdWhRyaPjj85i6IoX1KDH3j2VFxJPVXRCGbc3aumkhLZaAxwPamA_29_kDwZ1fwZH2NxrrTTz2fkj8OXqMfCWaM111Q7DjHudW1081Ty743Xvikz9OW19Tw0tQK5uZAJl8cWp7UGOFStTdIMBOVMEpQ57hyhQdqHLTf8pNgF5CyUwWVkxSsdVbTRUy6Fe5vQioAr19hHa_p3PpRntiQsBKGl5zhMuAOm7X59FAbkh1_f2FcJSO36U3FTxBEIH8_J-Vwfh_9XidCAZLuZu8-Zr4z8bJTi1-dL3xDMznPY2_Rumq1od8ax-Sycynrm6yHveQxYyVubF2o=w374-h667-no)
Listo! Ahora haremos que nuestro jugador pase por las plataforma y salte, ya que por los momentos simplemente es un cubo que rebota.

 Lo primero que tenemos que hacer es lograr obtener la información cuando se haga un toque de dedos o click en la pantalla. Hay muchas formas de obtener el resultado, yo usare las interfaces que trae Unity, pero tú puedes usar cualquiera de ellas.
 
  Lo primero que haremos es ir a *GameObject>Create>UI>Panel*. Al haber creado nuestro panel, tenemos que asegurarnos que el componente de *Image* tenga chequeado la caja de Raycast target. De esta manera, detectará la información del toque o click y se la pasará a nuestro panel. 

![enter image description here](https://lh3.googleusercontent.com/2P8t3EYmt_bBp4J0dXqHPnaCSG5aDHepviIj4DnuiVxLvgzPxhsb0DUBESphPlvbxCGGbt4a7OF5-dl43jxrOoRDavRtllSc0EayED45UuJKuKSDYml5gsZqRj8JbIdXXNFKom5awClj_obLvJ1EVItUdj3SfMTlLGCfGf_cKO8S_Vh6wgSnvWVMAoyiEgQ_x6p4N44OhhJrYjGPgW0HuSDM_ZO9qI2AAoxgBkpUqjM6tU3oaAWD5-C7ZBpbdMHwaVLntk0wZ0PBtYpK9TeBXsnhx0tYH_p8xVaB0d_oHTODyqITTlzedk3t1lQXHJqzIRcAakBQbKBQQtJwDCZNqzbn7R1S-OeR02DcnYOe5WC7JMN-t1P-TuwpMmlF6pDwW01LqsRpiLXZUII1zj6WI0_Ymuziexrs5ArlSAbqrVIXpWjKRl3jNrUJX4P0DIo_QqBCumoubk6N3lHNgxDRuHW5QJMn9oWDHV_0ywYdcaHYwJjWzQJCMiHaNkhzaytuJF1dnvsCYrlN3pPp-W2tDtxkiCGHK5g7rCFVv53NFl6_-ryMDTWJCq0luzJclwS3KIav6WB0ed5Gqv_99WKQYfM_XCNYjzA1OQmdrGECbE7H95VwIaxEDmDTN1Qv-CmgUlJzowi2WHLCyMuHyjbzNyjKNEA12b565ovDKq4VB-PebsZXOhuA16fJ03Piq1oEsrA-ZTm_9Y6n8deFuZPDqPfJ60F1sm3GqzwbdnwTQXJgn7A=w378-h664-no)
![enter image description here](https://lh3.googleusercontent.com/08meZhwv4A55kTzMTCYZXbFq8CBnL-6R75AUomnIyLcVJEvLp3zktRA0cdNwTrmVUYBWrCrawhuD4T1UZIAjYp0ZSdvB0ntkSIXsM9lDs_qYbyO7ae3U6fpLsRKFSkpJvAjmURNbJ46bH5j0cQv8_Vgr6JpgzsVgmOp-vfGyGGJK7rVKh-gHE2al8ach_hzs0o7NnWhzTp8hB23H_UprByeTlfUMQb2XbqBhJf8dgy76oOmSh0wJ41bHCj0Bd4DO0RXMNpbJFEPNfs0l6Pg0BBznAbMs1B556AaRj6E0LDBOG2eNLN7KyOipZ_Yy1rHc1iIpA2b_-09WgHvpYGZSgp1YQ1XTkRrzInmjDyUrcBoLR-p9R5uqZ4SRRj3rK96oDhi-Y4K4wlSqqkCMSW9tlPfvNGU8f0pvT_hyfLXQ9JckgCbvsKVLl6QbdIB67EWScM_KnTMc4tvlPRvJjPZ0oDjHGaMlH6TxpnePJO64TuygdRNpDIsxTIzePp3y-05y2ZKJ9CD5riIvEpNdeuCFUt3YZ8Fev7ErmeJhX6GDqyIYd4ehG3kD5wB0E1k5bJi9AgithKm0lKXqfZyj6WubKFyBVD1JrRs3Z_tV9pO6-_Jpix5i9np4QJIU_UpH9qjViTsvVYqH3mG7sXRXJahPzSTBY5z8-0U7GfUS2_U-3HVgybdwL7ybsUhtowVl601pGJGNMSdrZZPM3VAJ5FQ0eJDLdfmK6fj9kGc0hkXwiHSzuu4=w455-h526-no)
A este panel lo llamaremos InputPanel y luego crearemos un script llamado InputSystem. Este se encargará de tomar la información del toque o click y pasarla por referencia a cualquier otro script.

Para lograr usar las interfaces debemos usar librería de EventSystems. El EventSystem es una manera de enviar eventos a objetos en la aplicación basado en input, sea el teclado, mouse, tacto, o un input personalizado. En especial, nos interesa las siguientes interfaces para mas informacion te dejo los links:
> [UnityEngine.EventSystems](https://docs.unity3d.com/es/530/Manual/EventSystem.html)
> [IDragHandler  ](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/EventSystems.IDragHandler.html) 
> [IPointerDownHandler](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/EventSystems.IPointerDownHandler.html) 
> [IPointerUpHandler](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/EventSystems.IPointerUpHandler.html)



```csharp
using  UnityEngine;
using  UnityEngine.EventSystems; // importamos la librería

//Añadimos nuestras interfaces luego del MonoBehaviour con "," 
public  class  InputSystem : MonoBehaviour, IDragHandler,IPointerDownHandler ,IPointerUpHandler
{
	//Esta funcion se llama cuando es presionado el click.
	public  void  OnPointerDown(PointerEventData eventData)
	{			
	}
	//Esta funcion se llama cuando tienes 
	//presionado el click y lo mueves de un lado a otro
	public  void  OnDrag(PointerEventData eventData)
	{
	}
	
	//Esta funcion se llama al liberar el click
	public  void  OnPointerUp(PointerEventData eventData)
	{
	}
}
```
Luego de Implementar las interfaces añadidas, tenemos que empezar con la lógica. El primer problema a resolver es ¿Que tengo que comunicar a otros scripts?

 Primero definiremos nuestras variables, serán dos que son las que vamos a necesitar. Una para comprobar si estamos presionando o no la pantalla (IsPressing) y la otra es para saber cuanta cantidad de movimiento hay que aplicar para rotar al personaje (HorizontalDelta).
```csharp
	public bool IsPressing { get; private  set; }
	public float HorizontalDelta { get; private  set; }
```
Luego tomaremos la información que nos da la interfaz y la almacenamos en la variables que acabamos de declarar.
```csharp
	public  void  OnPointerDown(PointerEventData eventData)
	{
		IsPressing =  true;
	}
	
	public  void  OnDrag(PointerEventData eventData)
	{
		Debug.Log(eventData.delta.x); //Esto es para visualizar que tanta "fuerza" tiene nuestro arrastre 
		HorizontalDelta = eventData.delta.x;
	}
	
	public  void  OnPointerUp(PointerEventData eventData)
	{
		IsPressing =  false;
	}
``` 
Ahora pasamos a crear nuestro controlador, ya que tenemos una forma de obtener la información de la pantalla.

Para eso crearemos un script para mover nuestro jugador y lo llamaremos PlayerController.  Lo añadiremos a nuestro Player y agregaremos las siguientes lineas de código.
```csharp 
using  UnityEngine;

public  class  PlayerController : MonoBehaviour
{
	//Agregamos una referencia al input system mediante esta variable, para asi obtener la informacion de la pantalla
	public  InputSystem input;
	//Luego añadimos las variables para controlar nuestro jugador
	public  float speed;
	public  float rotationSpeed;
}
```
Ahora crearemos nuestra lógica de movimiento. Debajo  del mismo script colocaremos las siguientes lineas.
```csharp 
private  void  FixedUpdate()
{
	//Hacemos un early return cuando no se presione el panel
	if(!input.IsPressing) return;
	//Esta funcion nos mueve hacia adelante 
	transform.Translate(Vector3.forward * speed * Time.deltaTime); 
	//Luego comprobamos si nuestro delta es mayor(Es decir, si se esta arrastrando el dedo sobre la pantalla con cierta velocidad) a 0 y si lo es rotamos al presonaje
	if (Mathf.Abs(input.HorizontalDelta) >  0)
		transform.Rotate(Vector3.up, input.HorizontalDelta * Time.deltaTime * rotationSpeed);
}
```
A partir de ahora, podemos decir que el juego ya es jugable. Puedes comenzar a  modificar y probar valores a ver cual se siente mejor. ¡Siéntete libre de hacerlo!

No olvidemos que necesitamos nuestro InputPanel para tomar la referencia. Para lograr esto simplemente arrastra el InputPanel a la casilla de Input.
![enter image description here](https://lh3.googleusercontent.com/giOrbmyNFrlUwo8FICxjJEwtnjcvEJVCVS_9fjWDOKnYr-Un0ZmzBww3TUV_qWkC0P7-FFTNBxiPZiHvcIloao4Q5IxP3PXNK7kPsal3_HwpQE1nMGKoqaXZGEy9v5kkonj086XJeqYU6dPcyGW7Eo2V6UJNwzRBQCMGiMiZ6Cdl5xv6K6WwKa7QDAJW_XBl0FWj3PS2xg9W_CU-Pk9M4f-ltgJpljTnSDjURUrzV-l_JMoayEfuJLEyB6mpyoMpcwB0qPX0Ou0Gj5v9tLTgj8UkAfPK65GeoOP1F23SvkdRLZkb9oCdoWVV0bGviUrXIp-OE7wF2tYXvzwg_uWoF8hbJ1ZkcbdgR-F2NYyWfo3Y_GZbYI6uPgPxLgOXJuedmAYqjdR77POoqOEE18c78LkvBrN94pNVZGtlZi2pBLFYaBy4bMT7wyN2DcsayU1U3DG8oiYWTFb8T2I_oryKmQnB3TJOA0HoI-dzfHZk5xYQn1hQRR3JILkPYqPoNNkkShz8Ju9YE-RsqZSv53fUlWT2S-FbPE0nZaLPfQbitSX8vSS7SYAonO-yMWGw6xpZjJ8WyVYBc_pkUgt3KMgvFIlSziupKcIMcFNukxSOkSYcOWAVIQU3ZuFqjvBQ456gid-QuovIE06aNZAumK6ZucTzgUqzF00tDUo7VuR0es1FvRrkNd3mzXVyEF3igcXZ7skmC_3S-Win3B4ElpBSMy043_M4ijA54e0IkemaPRvyJWw=w462-h211-no)
![enter image description here](https://lh3.googleusercontent.com/Sb7qHqcfEy9uxVFqZjrzSFtoczDXa_z4MlGw6ZW1qpvOu-WU6wyQG2cKfwF-9pHCaW4ctdnMh-xrr32Ia6aIJ3DoJQj4s-ZLuV4-TeyQTAFY7VlMrgItyZpUTXRXLSSTw1T9GjEN4H7yZi2iu4XfgJVMZgeQgWufkRyEV0dnT51WDB5jYPlUGC98G7rVITXIKeUyDC0fII1PkJeMPwtlxokXKI_lzSpGnWXHq9p85IHIfgzZEQsY4TYVGYMyR6ENlsTsgqkXci4hXt1-IsBrPdgTxGrMl19EPnX7XwIUeF-yrPlFzIbhjW0xx3nFT-Tm_YkGcwZCY5qi_p9hYp18OVcGQShTligVStp3AnjxazfZUbXuG5tg91MKg5np1uzIg5tyeY3TT8SjxR0UvLPbXY-CnCcD3EBs97aj2Mf7bohpHIPbojJ16oeNjIrJp64dMnNo4E8r9OKejS8AG764l6gchKz58r1IbPv5jzmLw0rZLCLxdBNOqg6oN9hEtKLBpGzoYqeOMVQDMLWzlX3xRZsIjrUUItsMXShmkgLF0piuwWt0JNyNvQoQNfgELtiwr9C1DpTKO1I9KlgHJDR_NbTo4p3_H02qJctRA5FNNhLxAc1PudPaxcCLYEOd3FtE5zXWDcx-ET95UjwH7dbbK6zyS23wuv_TmWfqijKtTElCI4Tudn8fHkZTT27_0jU54C4H6EAktHyl6eaRVl1mLu29USaClI8HmZMjpxM5xZO0Ryc=w847-h385-no)
### Crea tu nivel
Ahora toma varios prefabs de trampolín  y ordénalos de manera de que el jugador siga un camino. En mi caso puse las plataformas hacia el frente y con  pequeñas curvas para probar la rotación del player, mientras seguían un camino de manera descendente.

![enter image description here](https://lh3.googleusercontent.com/mavjrsBSWnBp9CNkrLXtwJ_kq4_hum9MGKYPVCz5rrJM5RRFmE1QVKZFUlFSvpKUqiU0xF-TnyvB32YhaWM6ZiubrPSxgfXDXQRWTjo7zhecwFAj3KlRGHaYoEJO_l00vRU7oo6BHtwDFQ9eJ0i1IwIiqRGCJJtFj4_KPAxHx2YVqbanq_R9wi3Sdx7ioKr0jH-RVETuEVqStYqGqJzOw1wySrJxZwoLr3126yl9_Y3Mxq5D-XUAckv55kIMiYlZZcXgvAlXWkVmY1HMd50Kac_GoK836mxsowU2d1eFcEiZc_2yV4hz3AMk4ftA6ZKrKTUMdTcCU9BtIF6T3oPdmB-seEjSngeXuoh2oO0-HZy98q7q0vqvFqpPu0NVWbN7TfAn45NRco4_60JZMx_eBJkObmXkEauaMxQMsvszfKCgw1mEiAe1sf8xgYuhewDp6hzhrrGSe_aAHpS8xZ7IlTjDA_0bLXjWfzaxYUFLPrwOfQ0IsBFKmgrB-h7W7SG9EP13V6m814rPus25jeGp5Z5DpTNJpx7lda9R61VaOMha72ITIMY5dgOVvtGNCWOjYG7DsKWlZkRmu3h-jiyxcH5yeLiFnDnvJxSNHtL5mvl5b6dLi4vnHWw022loXJAPYZNhbHsFKfWjVqOFOqHrvZvoIC9PZe7RsieKvZJ3Mej7BHD7hIIYRIx3bh09UwfeLPNpjmjKwNVmIjcLEiuNCl1aMDmq6vHIt99GBk2gww5pjVc=w806-h667-no)
Ahora necesitamos crear un lugar para reiniciar el juego  en caso de que nuestro jugador se caiga al vacío. Para esto, crearemos la famosa killzone.

Para lograr esto crearemos simplemente un colisionador trigger que se accione al momento que el jugador pase a través de el.

Para esto, crearemos un Quad en *GameObject>Create>3d object > Quad*
y le cambiaremos el nombre a KillZone. Luego tendremos que ubicar nuestra zona muy debajo del mapa y aumentar su escala en el transform  unas 1000 veces, para asegurarnos que, no importa que tan lejos este el jugador, siempre colisione con la zona. 
![enter image description here](https://lh3.googleusercontent.com/YnYQa3ncFCOlnZqeSxt22FWwh5yo7AIHWW82hRXJq5EE5I_HvCd_Ylt07kFZ1yemhASJ7a0338tVsMHsMGfQ8RozSr627xbEPRj70otXnTWylDfsLzfNvIx35dZCv8QZft5DkymgHNo8wP-HucbggJUc62pv2rbbqxWVpJ4R3Fte5cxn-gXg_Iu3RLe17AB7reBYMpwhgHV64YGXsWEU4CsuMFK82c1Fsive5ltzEzoneJ6bKJxSmbqju8rtVwassE0148jDI6erMYNiTM-GQrzKM7_IabAdJ6VgDP-NsA7xOJmK2n3gRkgjQYa-6ULqkgc1TgBdTe3TnSGIhpwOeCPeULbjhVVMFc0IwWBwnMPkRp9fDgoUsJwf6hw7x9qoLavihjUH9qyAHNN6cJfz2-Ecy2RhBEM5beqI0F3Bt-zlxpEiZPh9p_wtGrDiqrQ94PcV5LaolmLfkrt9j2LQPGxsi7twkOmJAR1BryoNInDc7HVafGMGGgId0EIHaBi6uk-yK_tm2FQFwxuivr3M3VXKkZ-FVCFUmPW1lNchjsXEi3qy_hlSje2qzE65G09HMUbAlbUB9EU4u1ByhbCPI5NVDG2jEHB8YmOMmYGws6gtW9Vv9TpIERGc2l_w0JQS5jpVJzU0JKY0Aiz_mHP1faFgiFeVk9paWPEvyxPdRlJbk0H-0Ky-x4eXFIZ4g_iqqUkf36bHt9B708brcHnpPkqAdOWQHqYCHWTeHGbS82L0LPc=w924-h667-no)
Luego añadiremos un nuevo script para lograr este objetivo. No olvides chequear el mesh collider como convex y chequar el trigger.
```csharp 
using UnityEngine;
using UnityEngine.SceneManagement;

public class KillerZone : MonoBehaviour
{
	private void OnTriggerEnter(Collider other)
	{
	//Simplemente si detectamos que el trigger que colisiona es un player, reiniciamos la escena.
		if(other.GetComponent<PlayerController>() != null)
			SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
	}
}
```
Luego añadimos la escena en *File > buildSettings*.
![enter image description here](https://lh3.googleusercontent.com/PI41A_joVb2dqefWjKMVX2ilsy7JZ2Or7oAEG6yI3Z58KPc8N1bYdX1yIi5e1xwq-feKTYUSAZlUbb40Wh_QYs_rkCBH3pA_q86jxKfTJhDEG81evBQReHBbIjDO8aIXYhrpKgq6kuWk7jH6--gW3Ihp3KT6tMxwztYeaniBjLdFv3P59yenDlqOvYixZ0SOoLhLuyWVMtVnb85IlRdThj6Wx7-I4FM26BJJeRlfdnp2CN4cFSGjdZ92kgKuvD9fhczkPmEAZ0f3SX8umRe8cH3JD3rq1fO931EwV8hN-U6KMexZUVEh87KSaBL3XLzYvFpJEjfLxb6XVKbBuica6eIXpNIywHJQfS01MSjrAldig6GgNbhB68-wh_3riOKek-e-2u3ooPPn6j1d0KadnwVW08Q18yjXDcV-UVuFqmrueK4wSfdBsl3faHoDI2PHNF2klR-OFPlbBipgNU9Ke_e1Ldul2fFZRpfAzuHdjaaDT37aE143Adqtv6qEbTSp5tZ42D-eFhtCOcxjiRHzeMgBL4oFqE_Hj9uBWtvC2dYpnp-xGnDfT-VmNh6780PBbyQNHEgh5SL3rCvTUnliZwuVHIQpaYqRh6qym7YSgSWWpnH5shvME4R4s6Mli2PPS953oOrTEM1FbGPwiNfO1kW9ggYrUd1cSdQu07DLYORphdf3TsoSUN_WLbATGOMSRAsQQadtp9KtKYMfMeJKJe7CatFv8DkkEgjbxBt2rUNZ2_4=w633-h588-no)


### Algunos Ajustes extras
Hize algunos cambios al iterar varias veces en la mecánica, pues me di cuenta que algunos valores se sentían mejor que otros. Aquí dejo las correcciones:
>Valores de la cámara
![enter image description here](https://lh3.googleusercontent.com/Lj4v76UyNZRCYRPfOFlwNrVjp17SlN0tpULeUD-V6kfkUZcsHd11G0KS3JSHF7ImR944d306Q0P1DPlQ4UJmqhnY2Dk-1PG9lfHouRruRj7jQgwlcf2P8_2aXMmy3kMnwHwDvzyfkqB2fbnAuHfHAZVrHTKpUMzaxxpzJCY_gKLMa2kFAKswBPCfwwuJnJwNCyYozGSOk7o-WTyG8o4Cryz6k0e3JuIKCT7uAhuaqtnuEujim-siAwUJ_bzXaweesszL5lNebCp_icDulXPMBJyBTkAKetIQBPWSsCfMlghPT6CzIO-heIKVgPCUwFOV4z7N6Y3y3pHOhxTFA97uqNFSiA5bayNi4vWzyt4mFMwMBsLz8PTcrF9F2vL43OlonQ4KlM8chV9RIo52l-B4aN638mvQX2tHoQSt3NmkQOplXxVynZvMdV_PL5vUrcHf_Zbo2jTD-ZEsAWUC80JcjMpXtLBqGsB4qwbm-4QOWpjTq0ei1i_GmcwFG_LRMwDMoTgeFY3IQZuPObMLA2qHYMmG1ebDpZs1ztU0hDYAX2XBDI-P7qGccmt_xg5H6Fi8bcQm0Uvzov73DTTKlkkl2CavDMyd2ow4lDAp22c53aw8EZClEdQ0Hev8s1ouC7w0RuJ7GsCKfZ5FZjYQGcNAUJgPBETamjKsVEwT9UuJD4wRq0A_ggj_CPueYbp4jxVBvjEYy-op7o2uHXzGRaNNvOAZiKZbBVXkTs05M-N2ClWU3MQ=w460-h145-no)

>Valores del Player controller 
> ![enter image description here](https://lh3.googleusercontent.com/1dulE-BQSs2xeMs_x5epoz1XxfzFePQ7vzHSJqIyJuYK4WjvuV8ynnyrONYGwH-MwSbmS69-aQ1ND49jgi4C_K8kwrI7CGvLhXPMvLsHxmrdho03jFC09vvjQIUV9ehDc8BQ8Z29wPN6u6AW3Tajsj85loayzqj3jUr1LNiMy_09U2HT18o7cVzQkuRddda0Ip0VFHvmS0sb5_nTgv1QmjPy0K0NO8B9JnOfgL6EQhU_OFWJ9XwLgR4dCwKGEALGTuVoMZU3rmJTa2aVFhDO2LYaCTeK9k0QqTM05khQ1-0dDWzaNC-bU5JG_JN-HHMw0knUQtyIY3VZTOEv2V6jk0Yc0TnE7xNRDSPHishn5y3rB9gfcwP0k8ZFEW59URqL7b4lo0XyQyDF1hVTQk2kaUC4TlFQCBcSCQvYz7YDeEU8OrHD9ufsInLiSowWLN9K8KDoWLE8JQUrl0js8t6fLLibm3cRA5L1QU7gmborQ116Ky_u4q9iiH9zLcVgaAVPWhcRZJJTDJY5uWVqJ3FzGwe7N09YEFyRUyHzsRNo1obtv7T8PfbU7atTf3bY3cBsm_NjCHTdrbxJWfULMdICcjZOzsn3Gb__KZNFoChmB62FsUyN5tc4dLNUU-a412vaksBgi20rzD5b2kAI9-GazBowMNo8EkQus_WQBc4AOcqpjwKuEd7vnDJ8tzYn0SFqUAQ1wQQqzv73LPPwHPPKkRSwF3jJNBHuxtWoIaO4MeTCdM4=w453-h96-no)

>En el script de Input system añadí esto:
``` csharp
public  void  OnPointerDown(PointerEventData eventData)
{
	IsPressing =  true;
	//Ahora la velocidad se reseteará cada vez que se presione la pantalla.
	HorizontalDelta =  0;
}
```


Crea un nuevo script para el Player controller, para añadir una mejor sensación al estar cayendo y que el movimiento de la caída no se sienta tan  lento. 
![enter image description here](https://lh3.googleusercontent.com/K9Jznc4RR0pgcXoN5UdM5joYbd2mYqj8Jiu6jqM4BDHBoYtqpUUk-lWSK6gcwHrRyxlxHxZpkrnmgiulvBq6-iVF7vFE6XjK0Ha03ds51AdR71jMCsLAl2LDqjJEXrq0iZKoDm4h1SsqD1mOaOM_HtvrEWgmOUz0dFIt7Ex7kDc_4eVsayQiBq0jURGL3GbuEJz6J5Lew2BF89NkDKh9SenIBsswQHpLw2iGxoecvw5zNSmbacfNcRS6uj8XFo68FuNyncM_8KVF2gvUHfmGc_s0yoxCtvhAGbetoMi62QskKMN0K7CVHky4UzTOUDuhXUtn8rZn3NGWs6QMkDACy5dOcmw0bJWZouK8Nf4PmZfiZDLVWVyHwzqckZD_LKlVEJZJbj0kNdvK2E22sZV8rOdxew9kc2AJtbyZn3PTY95e-6IypskJObrkPgYsyZDRbP6GllV-R1fglfsNLvK6lN0dQ5DA_yNnmYuPvJwB7_QyXx4NWxH9fgIP1WBujDtRnz1RaoJoHyNfkjyaw9qAA1ObJlEVkvPee_TkgDpVoEn9xu5kBHZq6zsxJamuSD01GyR4EQdbMVL2hCx64z8IKus31jnvWc31KQYdzWIRETmQ5NSlTlne2Xeyzu334oR9yga6FW_nN-CDhzDcJoep_AZ1DTfTNp5dJwWambSHw0ywgWhrHFN27vWCBxvlwJ4_Nupnx2kbIFx5204ApQuqbmhHQXKr8wAoEWUPW4wc873Xor0=w845-h665-no)

``` csharp 
using  UnityEngine;
public  class  BetterFall : MonoBehaviour
{
	public  float fallMultiplier =  2.5f;
	public  Rigidbody rb;
	private  void  FixedUpdate()
	{
		if (rb.velocity.y <  0)
		{
		//Esto ayuda a caer mas rapido
			rb.velocity += Vector3.up * Physics.gravity.y *(fallMultiplier -1 ) * Time.deltaTime;
		}
	}
}
```
![enter image description here](https://lh3.googleusercontent.com/FTeMkesgzUpUKx40yt1aSvA2CUMSroC9yzfJoXMseasImmYlfVk_V7nyrTmaoVSoo-3wUBWDQpVyLZi8TC9X2B1luPtoCJD9XnDPr4uczfdhuF2Dj55fZm38nsVb6rMl-AmKdhNl85PTkX85rMw9wMoKyeIw8qBAA3FWT-KclBZUPMkqS6vx6oR6x6kM6kLHEOkOqV7NGEElcCI3h87igYB_IlB8BTOaqKxBCEOJzJE5HeoRL3y_Vq4cO7TMror2vQt_F7MrgVtzE0eJ-gJhwgTCHKrYYDTjti0jvJg0Dqz5vReYTvDspS6C5ywwBNl4I37iSTXG6PcjD3ITPO23grUqCy-95UaZamlvJy_0cbQnt5vTCqEdwk34kqDxI4obpWbkHnJbgUlJJbfvyPT5vEi9Ybhiv8UUH-ulxA5LBrdcSGEsey5GyNYzIcSkG1cBApdyYuh61gwwgsROLXzAYt0oAZgocLoxCHpZ6-q9wmJ8DexQ5sER5UCg8xkJlmIjWGp2mxae-tJsv2YwUYpUDsKu8EGdX8srWxUevo4QUIYDjkwJ3DHtRquJj1oCh5KRQ_IdqSU1bWHv2R4jWaqEFam8Mw_9tjQM2EMQSdJD73fVW7fDrCahEM6vZ7POyf7SyiUVdqgySP5mymkAHtwt1IHvGaZPiVQNur65_GS87QFRBased8qB24HFe5Nz-CCJ3xkwUKnA2XLE2Z7Hj9V7iG4fyuNfjCzVRqvaocN5yJ8KVrQ=w450-h85-no)

### ¡Haz tú primera build!
Asegúrate de tener la orientación de Portrait en playerSettings.
![enter image description here](https://lh3.googleusercontent.com/45f6PPIqC4e-sE90dOzgPTWpEVJgeKp_NTGXkZ-boiba7MEUp7Mmdp149Gkil11S2Y1JPapH5XD0s_7G5wHaonQbsYb5DB1lgVSt7l5XVr-SJO_YTP6j0TElwXaT9nm-u6PCD5c5mFQmXV6itxj2k9rXLgfVeEg-0XuPL6539B7CwCoNaVCEipPNmlwv4_EBfuCt0Z51v7X7G5hMI3jit9fXYO7_XdqyJSUp4ex00omYq4f7td_IBppqOhwvdeNFptqoyqnc773vq6ewFalfVIMBz1fYy85zxNWBz_oJYzhQ-IjoLqROxmRWYEiYjEvVpR24D2zkfd6xpguP1l1PMpdmtxKq1xqwWGA2yvqH-UdxUW0WwpJxnsXLJOgaqUuXVbyAeiFmIwiShPl-iMASWnNu8WStNKviT__CqOqOXWLlufvmc4Z9E9bv8q5rWSR720z82hYJ2yMN8Uvuv2DeHrq3TXtwh4atFX-7PLAlbh6JhVLVVX5RoHv4vbySCeP9ISuHubrCIJjaFmykchfWsWzR_Sh6K_0LAWX6wk-lfwxse4aLb63Pfim_urXKojCiHDiEDRNSlmW64SUQVjRzSucd1A0exOkhVcRqGbqhjoUZWPh36XbqPcitoeD0En2_2Wfw9yJ_enn5EQdpZA1hAIlt-5M7dzZxvu2arZgto89PHiNo8oH6XTnwMfT7No45d3tsTf4MgRusSERYKLNmwfwciB-XQYFYAz0GAQ_F9o4kLVw=w442-h307-no)
![enter image description here](https://lh3.googleusercontent.com/Ddv2Y6ExpbYJgDdx8qY8UrAQTfvM54uHbtYiZ-h1XOtW1hg_yEqvL9P-I3JtZXqNvBIyUNkTe8QqMtKpHnkNZa2i5kT7yj1dsbW7dtRcnE-wHyOSQ0ji9ZZAi0wwcEAchr5_mBUAElB5eQDkA5jOUbDlGIBB8UUMUJbK9FYJl22kp2V48KGlErkcnLC4RPP2U0oAeCJBGimiWyE1L1q8spvZjeKAuQuYe8x5cqCKSlzcQ3FUMQF28dBK3fV9Oq0OPZkvftwIfD6xMlKbaZb9R46l_dbtoVX8xjkZ942Ls0SBbTUOVbetyrA3yh_L-fr5mpzNGLag13cuWzSfw8V9Gooslalt3_XKX_oXGJXR5Td9Phrqd0zUPhKAXWkNBe-w_qA0LXsnq4SkUL8eU8Z7_BANEjc0pMuuaH2FIcGS1ACG7TNrHtz1CZdG3WDPEk7fVqActydribRxcZURXDZnYLKW0-Nl9vTw8BF0ThQ1gR9mLEuYFFyiZOC6gNS8H-K8PT__OwBAwZowrWgyqzgDB54tsXcSWAMgMOcIdyPJISfLI_2X7dlOgGREldskNg_PNJGcCd6ngEHj9Ukryx-DIXlV-P-ZdHykc0AGJgmEM0ZCV6vAPL19xQBKQnagdofs0g7Ex710bsOj1krpYAzj3SwUuKfj-qwvJbpi-dTCQKS1JT1QzlvcJQ=w643-h614-no)

¡Felicidades! Ahora tienes un prototipo funcional que puedes usar para mostrárselo a tus profesores o compañeros. Puedes crear varios niveles y probar hasta donde puede llevarte esta mecánica, sin embargo este no es el fin.
  
  Ahora que ya hemos terminado gran parte del apartado mecánico, en el siguiente tutorial pasaremos a la parte artística. Agregaremos un personaje modelado unas animaciones y mas cosas interesantes!

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZmVhdHVyZWRJbWFnZTogJ2h0dHBzOi
8vZHJpdmUuZ29vZ2xlLmNvbS9vcGVuP2lkPTFWb0tCTENJTUdI
YnRzdDlyZFdrUnN5bEZwN3dpVjVZOCdcbiIsImhpc3RvcnkiOl
sxNjc4NDUxNTQ1LDExMjI3MTQ1NDMsLTQ2MjE3MDcxMCw4MjAx
NTM3MDAsNzk2MDYyOTUxLDYzMzQ4MDY1NywtNDAzMjE1MTk2LD
E3ODIyOTc2MDUsMTE4OTEzMDE5NSwtMTMzNDUzNjgwLC0zNjQz
MTI0NTYsMjE0MDU3MTY0Nyw4MzgwNzk5MjYsMTc4NTAzMTk2My
wtMTQ1OTQ3ODYyLDc4MTQ0MDI5NiwtODAzNDEwODkzLC0xODc2
OTYwODU4LDU1Mzk3MTcwMiwtMTcwNTk1NTQ3NV19
-->
