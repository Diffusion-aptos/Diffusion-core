```
import React, { useEffect } from 'react';
import anime from 'animejs';
import './LogoAnimation.css';

const LogoAnimation: React.FC = () => {
  useEffect(() => {
    anime({
      targets: '.ball1',
      translateY: [
        { value: -300, duration: 1000 },
        { value: -250, duration: 1000 },
      ],
      translateX: [
        { value: 50, duration: 1000 },
        { value: 0, duration: 1000 },
      ],
      easing: 'easeInOutSine',
      loop: false
    });

    anime({
      targets: '.ball2',
      translateY: [
        { value: -300, duration: 1000, delay: 500 },
        { value: -250, duration: 1000 },
      ],
      translateX: [
        { value: -50, duration: 1000, delay: 500 },
        { value: 0, duration: 1000 },
      ],
      easing: 'easeInOutSine',
      loop: false
    });

    anime({
      targets: '.ball3',
      translateY: [
        { value: -300, duration: 1000, delay: 1000 },
        { value: -250, duration: 1000 },
      ],
      translateX: [
        { value: 0, duration: 1000, delay: 1000 },
        { value: 0, duration: 1000 },
      ],
      easing: 'easeInOutSine',
      loop: false,
      complete: () => {
        // 最後一步，顯示最終的logo
        anime({
          targets: '.logo',
          opacity: [0, 1],
          duration: 1000,
          easing: 'easeInOutSine'
        });
      }
    });
  }, []);

  return (
    <div className="logo-animation">
      <img src="/path/to/ball1.svg" className="ball1" alt="Ball 1" />
      <img src="/path/to/ball2.svg" className="ball2" alt="Ball 2" />
      <img src="/path/to/ball3.svg" className="ball3" alt="Ball 3" />
      <img src="/path/to/logo.svg" className="logo" alt="Logo" style={{ opacity: 0 }} />
    </div>
  );
};

export default LogoAnimation;
```
```
.logo-animation {
  position: relative;
  width: 400px; /* 根據你的需要設置寬度 */
  height: 400px; /* 根據你的需要設置高度 */
  margin: 0 auto;
  overflow: hidden;
}

.ball1, .ball2, .ball3 {
  position: absolute;
  bottom: 0;
}

.logo {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```
`import LogoAnimation from './LogoAnimation';`

```
/* MyMenu.css */

#outer-container {
  perspective: 1500px;
}

#page-wrap {
  transition: transform 0.5s;
  transform-origin: 100% 50%;
  position: relative;
  z-index: 2;
}

.bm-menu {
  background: #373a47;
  padding: 2.5em 1.5em 0;
  font-size: 1.15em;
}

.bm-item-list {
  color: #b8b7ad;
}

.bm-item {
  display: inline-block;
  color: #d1d1d1;
  margin-bottom: 10px;
}

.bm-burger-button {
  position: fixed;
  width: 36px;
  height: 30px;
  left: 36px;
  top: 36px;
}

.bm-burger-bars {
  background: #373a47;
}
```
`https://medium.com/geekculture/how-to-use-google-analytics-on-reactjs-in-5-minutes-7f6b43017ba9`


framer 教學
```
https://motion.framer.wiki/action-drag
```


計時
```
import React, { useState, useEffect } from 'react';

const CountdownTimer = ({ expiredDate }: { expiredDate: string }) => {
  const [timeLeft, setTimeLeft] = useState<string>('');

  useEffect(() => {
    const calculateTimeLeft = () => {
      const now = new Date();
      const day = parseInt(expiredDate.slice(0, 2), 10);
      const month = parseInt(expiredDate.slice(2, 4), 10) - 1; // JavaScript months are 0-based
      const year = parseInt(expiredDate.slice(4, 8), 10);

      const expirationDate = new Date(year, month, day);
      const currentDate = now;

      let timeDifference = expirationDate.getTime() - currentDate.getTime();
      if (timeDifference < 0) {
        timeDifference = 36 * 60 * 60 * 1000;
      }

      const totalSeconds = Math.floor(timeDifference / 1000);
      const days = Math.floor(totalSeconds / (3600 * 24));
      const hours = Math.floor((totalSeconds % (3600 * 24)) / 3600);
      const minutes = Math.floor((totalSeconds % 3600) / 60);
      const seconds = totalSeconds % 60;

      setTimeLeft({ days, hours, minutes, seconds });
    };

    calculateTimeLeft();
    const interval = setInterval(calculateTimeLeft, 1000);

    return () => clearInterval(interval);
  }, [expiredDate]);

  const containerStyle: React.CSSProperties = {
    display: 'flex',
    justifyContent: 'space-around',
    alignItems: 'center',
    fontFamily: 'Arial, sans-serif',
    fontSize: '1.5rem',
  };

  const itemStyle: React.CSSProperties = {
    textAlign: 'center',
  };

  const numberStyle: React.CSSProperties = {
    fontSize: '2rem',
    fontWeight: 'bold',
    marginBottom: '0.5rem',
  };

  const labelStyle: React.CSSProperties = {
    fontSize: '1rem',
    color: '#555',
  };

  return (
    <div style={containerStyle}>
      <div style={itemStyle}>
        <div style={numberStyle}>{timeLeft.days}</div>
        <div style={labelStyle}>Days</div>
      </div>
      <div style={itemStyle}>
        <div style={numberStyle}>{timeLeft.hours}</div>
        <div style={labelStyle}>Hours</div>
      </div>
      <div style={itemStyle}>
        <div style={numberStyle}>{timeLeft.minutes}</div>
        <div style={labelStyle}>Minutes</div>
      </div>
      <div style={itemStyle}>
        <div style={numberStyle}>{timeLeft.seconds}</div>
        <div style={labelStyle}>Seconds</div>
      </div>
    </div>
  );
};

export default CountdownTimer;


```

