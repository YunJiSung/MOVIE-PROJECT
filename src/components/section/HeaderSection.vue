<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <h1>Movie Site</h1>
                <nav>
                    <ul>
                        <li><a herf=""></a>추천 영화 Top10</li>
                        <li><a herf=""></a>코딩 영화 Top10</li>
                    </ul>
                </nav>
            </div>

            <div class="header__intro"
                style="backgroundImage:url(https://image.tmdb.org/t/p/w500/kjQBrc00fB2RjHZB3PGR4w9ibpz.jpg)">
                <div class="container">
                    <div class="left play icon">
                        <a href="#">
                            <img src="https://image.tmdb.org/t/p/w500/vFsSluuzqxR46Ils9ib52ItdE9u.jpg" alt="">
                        </a>
                    </div>
                    <div class="right">
                        <h2>"The Creator"</h2>
                        <p class="desc">"인류를 지키기 위해 만들어진 AI가 LA에 핵폭탄을 터뜨린 후, 인류와 AI 간의 피할 수 없는 전쟁이 시작된다. 전직 특수부대 요원 ‘조슈아’는
                            실종된 아내의 단서를
                            얻을지도 모른다는 생각에 전쟁을 끝내기 위한 인류의 작전에 합류한다. 인류를 위협할 강력한 무기와 이를 창조한 ‘창조자’를 찾아 나서고, 그 무기가 아이 모습의 AI 로봇
                            '알피'란 사실을 알게 되는데… 인간적인가, 인간의 적인가? 10월, SF 블록버스터의 신세계가 펼쳐진다!"</p>
                        <p class="date">개봉 : 2023-09-27</p>
                        <p class="average">평점 : 7.1</p>

                        <div class="credits">
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/qoOp8XvZ4v7B0C9ZmtoRCl9CDSO.jpg"
                                    alt="John David Washington">
                                <img src="https://image.tmdb.org/t/p/w500/mLKvNuCJSgyK0WdLd4ogO81sOO1.jpg"
                                    alt="Madeleine Yuna Voyles">
                                <img src="https://image.tmdb.org/t/p/w500/lm2FKwj2zO8ZsqMNFHm4KMtlNlM.jpg" alt="Gemma Chan">
                                <img src="https://image.tmdb.org/t/p/w500/cDcB8mKP1GiIeoM3Qe7GIucs0iv.jpg"
                                    alt="Allison Janney">
                                <img src="https://image.tmdb.org/t/p/w500/w2t30L5Cmr34myAaUobLoSgsLfS.jpg"
                                    alt="Ken Watanabe">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<style lang="scss">
.header__inner {
    justify-content: space-between;
    align-items: center;
    padding: 1rem;


    .header__nav {
        display: flex;
        justify-content: space-between;
        align-items: center;

        h1 {
            font-size: 24px;
            color: var(--black);
            font-family: '';
            padding: 5px 1rem;
            margin: 20px 10px;
            border: 1px solid var(--black);
            display: inline-block;
            text-transform: uppercase;
        }

        nav {
            li {
                display: inline;

                a {
                    display: inline-block;
                    padding: 10px;
                }
            }
        }
    }

}

.header__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        backdrop-filter: blur(10px);
        z-index: 1;
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
            width: 350px;

        }

        .right {
            width: calc(100% - 390px);

            h2 {
                font-size: 30px;
                margin-bottom: 10px;
            }

            p {
                margin-bottom: 5px;
            }

            .desc {
                margin-bottom: 10px;
            }

            .credits img {
                width: 100px;
            }
        }

    }


}
</style>