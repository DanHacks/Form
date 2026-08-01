# Formimport { useState, useEffect } from 'react';

export default function AnimatedCounter({ end, duration = 2000, suffix = "" }: { end: number, duration?: number, suffix?: string }) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    let startTime: number;
    const animate = (timestamp: number) => {
      if (!startTime) startTime = timestamp;
      const progress = Math.min((timestamp - startTime) / duration, 1);
      setCount(Math.floor(progress * end));
      if (progress < 1) {
        requestAnimationFrame(animate);
      }
    };
    requestAnimationFrame(animate);
  }, [end, duration]);

  return (
    <span
      role="status"
      aria-live="polite"
      aria-label={`${end}${suffix}`}
      className="tabular-nums tracking-tight"
    >
      {count}{suffix}
    </span>
  );
}
