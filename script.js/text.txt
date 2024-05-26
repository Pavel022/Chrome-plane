document.addEventListener('DOMContentLoaded', () => {
    const airplane = document.getElementById('airplane');
    const skyscraper1 = document.getElementById('skyscraper1');
    const skyscraper2 = document.getElementById('skyscraper2');
    let isFlying = false;
    let gravity = 0.9;
    let speed = 5;

    function fly() {
        if (isFlying) return;
        let position = 0;
        isFlying = true;
        
        let upInterval = setInterval(() => {
            if (position >= 150) {
                clearInterval(upInterval);

                let downInterval = setInterval(() => {
                    if (position <= 0) {
                        clearInterval(downInterval);
                        isFlying = false;
                    }
                    position -= 5;
                    position *= gravity;
                    airplane.style.bottom = position + 'px';
                }, 20);
            }
            position += 30;
            position *= gravity;
            airplane.style.bottom = position + 'px';
        }, 20);
    }

    function moveSkyscrapers() {
        let skyscraper1Position = 200;
        let skyscraper2Position = 0;

        let leftTimer = setInterval(() => {
            if (skyscraper1Position < -40) {
                skyscraper1Position = 600;
            }
            if (skyscraper2Position < -40) {
                skyscraper2Position = 600;
            }

            if (
                (skyscraper1Position > 0 && skyscraper1Position < 90 && parseInt(airplane.style.bottom) < 100) ||
                (skyscraper2Position > 0 && skyscraper2Position < 90 && parseInt(airplane.style.bottom) < 100)
            ) {
                clearInterval(leftTimer);
                alert('Konec hry!');
                document.location.reload();
            }

            skyscraper1Position -= speed;
            skyscraper2Position -= speed;

            skyscraper1.style.right = skyscraper1Position + 'px';
            skyscraper2.style.right = skyscraper2Position + 'px';
        }, 20);
    }

    moveSkyscrapers();

    document.addEventListener('keyup', (e) => {
        if (e.code === 'Space') {
            fly();
        }
    });
});