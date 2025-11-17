import React, { useEffect, useRef, useState } from 'react';
import { Github, Linkedin, Instagram, Twitter, Mail, Star, Code, Database, Cpu, Zap, Sparkles } from 'lucide-react';

const CinematicGitHubProfile = () => {
  const canvasRef = useRef(null);
  const [scrollY, setScrollY] = useState(0);
  const [mousePos, setMousePos] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    const handleMouseMove = (e) => {
      setMousePos({
        x: (e.clientX / window.innerWidth) * 2 - 1,
        y: -(e.clientY / window.innerHeight) * 2 + 1
      });
    };

    window.addEventListener('scroll', handleScroll);
    window.addEventListener('mousemove', handleMouseMove);
    return () => {
      window.removeEventListener('scroll', handleScroll);
      window.removeEventListener('mousemove', handleMouseMove);
    };
  }, []);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const particles = [];
    const particleCount = 150;

    for (let i = 0; i < particleCount; i++) {
      particles.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        vx: (Math.random() - 0.5) * 0.5,
        vy: (Math.random() - 0.5) * 0.5,
        size: Math.random() * 2 + 1,
        opacity: Math.random() * 0.5 + 0.3
      });
    }

    let animationId;
    const animate = () => {
      ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      particles.forEach((p, i) => {
        p.x += p.vx + mousePos.x * 0.2;
        p.y += p.vy + mousePos.y * 0.2;

        if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
        if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        
        const gradient = ctx.createRadialGradient(p.x, p.y, 0, p.x, p.y, p.size * 3);
        gradient.addColorStop(0, `rgba(99, 102, 241, ${p.opacity})`);
        gradient.addColorStop(0.5, `rgba(139, 92, 246, ${p.opacity * 0.5})`);
        gradient.addColorStop(1, 'rgba(236, 72, 153, 0)');
        
        ctx.fillStyle = gradient;
        ctx.fill();

        particles.forEach((p2, j) => {
          if (i === j) return;
          const dx = p.x - p2.x;
          const dy = p.y - p2.y;
          const dist = Math.sqrt(dx * dx + dy * dy);

          if (dist < 120) {
            ctx.beginPath();
            ctx.moveTo(p.x, p.y);
            ctx.lineTo(p2.x, p2.y);
            ctx.strokeStyle = `rgba(139, 92, 246, ${0.15 * (1 - dist / 120)})`;
            ctx.lineWidth = 0.5;
            ctx.stroke();
          }
        });
      });

      animationId = requestAnimationFrame(animate);
    };

    animate();

    return () => cancelAnimationFrame(animationId);
  }, [mousePos]);

  const techStacks = [
    { name: 'Frontend', items: ['React', 'Next.js', 'TypeScript', 'Tailwind', 'Flutter', 'React Native'], icon: Code },
    { name: 'Backend', items: ['Node.js', 'Express', 'Python', 'PHP', 'Firebase'], icon: Database },
    { name: 'AI/ML', items: ['TensorFlow', 'Hugging Face', 'OpenCV', 'NumPy', 'Pandas'], icon: Cpu },
    { name: 'Cloud', items: ['Firebase Studio', 'Vercel', 'GCP', 'Azure', 'Cloudflare'], icon: Zap }
  ];

  const projects = [
    {
      title: 'Aicademy',
      desc: 'AI-powered learning platform with course generation',
      tech: 'Next.js • Gemini • Drizzle • Tailwind',
      gradient: 'from-violet-600 to-indigo-600'
    },
    {
      title: 'GrowTo',
      desc: 'Animated agriculture company landing page',
      tech: 'Next.js • Framer Motion • Tailwind',
      gradient: 'from-emerald-600 to-teal-600'
    },
    {
      title: 'Smart Home AI',
      desc: 'Intelligent home automation system',
      tech: 'TensorFlow • OpenCV • React Native',
      gradient: 'from-pink-600 to-rose-600'
    }
  ];

  return (
    <div className="min-h-screen bg-black text-white overflow-x-hidden">
      {/* Animated Background Canvas */}
      <canvas ref={canvasRef} className="fixed top-0 left-0 w-full h-full pointer-events-none z-0" />

      {/* Hero Section */}
      <div className="relative z-10 min-h-screen flex items-center justify-center px-4">
        <div 
          className="text-center"
          style={{
            transform: `translateY(${scrollY * 0.5}px)`,
            transition: 'transform 0.1s ease-out'
          }}
        >
          {/* Glowing Avatar */}
          <div className="relative inline-block mb-8">
            <div className="absolute inset-0 bg-gradient-to-r from-violet-600 via-purple-600 to-pink-600 rounded-full blur-2xl opacity-60 animate-pulse" />
            <div className="relative w-40 h-40 rounded-full bg-gradient-to-br from-violet-500 via-purple-500 to-pink-500 p-1">
              <div className="w-full h-full rounded-full bg-black flex items-center justify-center text-6xl font-bold bg-gradient-to-br from-violet-400 to-pink-400 bg-clip-text text-transparent">
                MA
              </div>
            </div>
          </div>

          {/* Name with cinematic effect */}
          <h1 className="text-7xl md:text-9xl font-black mb-4 relative">
            <span className="absolute inset-0 bg-gradient-to-r from-violet-600 via-purple-600 to-pink-600 bg-clip-text text-transparent blur-lg opacity-50">
              MOHD AMAN
            </span>
            <span className="relative bg-gradient-to-r from-violet-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
              MOHD AMAN
            </span>
          </h1>

          <div className="space-y-2 mb-8">
            <p className="text-2xl md:text-3xl text-gray-300 font-light tracking-wider">
              Full-Stack Developer • AI Architect
            </p>
            <p className="text-xl text-violet-400 font-mono">
              Building the Future with AI & Code
            </p>
          </div>

          {/* Social Links */}
          <div className="flex gap-4 justify-center mb-12">
            {[
              { Icon: Github, href: 'https://github.com/MohammadAmannn', color: 'hover:text-violet-400' },
              { Icon: Linkedin, href: 'https://www.linkedin.com/in/mohd-aman-021261236/', color: 'hover:text-blue-400' },
              { Icon: Instagram, href: 'https://www.instagram.com/oyie.aman', color: 'hover:text-pink-400' },
              { Icon: Twitter, href: 'https://x.com/wtf__ammu', color: 'hover:text-sky-400' },
              { Icon: Mail, href: 'mailto:itsaman00786@gmail.com', color: 'hover:text-red-400' }
            ].map(({ Icon, href, color }, i) => (
              <a
                key={i}
                href={href}
                target="_blank"
                rel="noopener noreferrer"
                className={`p-4 rounded-full bg-white/5 backdrop-blur-sm border border-white/10 ${color} transition-all duration-300 hover:scale-110 hover:bg-white/10 hover:shadow-2xl hover:shadow-violet-500/50`}
              >
                <Icon size={28} />
              </a>
            ))}
          </div>

          {/* Scroll Indicator */}
          <div className="animate-bounce">
            <div className="w-6 h-10 border-2 border-violet-400 rounded-full p-1">
              <div className="w-1.5 h-3 bg-violet-400 rounded-full mx-auto animate-pulse" />
            </div>
          </div>
        </div>
      </div>

      {/* Tech Stack Section */}
      <div className="relative z-10 py-32 px-4">
        <div className="max-w-7xl mx-auto">
          <h2 className="text-6xl font-black text-center mb-20">
            <span className="bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">
              TECH ARSENAL
            </span>
          </h2>

          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
            {techStacks.map((stack, i) => (
              <div
                key={i}
                className="group relative bg-gradient-to-br from-white/5 to-white/0 backdrop-blur-xl rounded-3xl p-8 border border-white/10 hover:border-violet-500/50 transition-all duration-500 hover:scale-105"
                style={{
                  animation: `float ${3 + i * 0.5}s ease-in-out infinite`,
                  animationDelay: `${i * 0.2}s`
                }}
              >
                <div className="absolute inset-0 bg-gradient-to-br from-violet-600/0 to-pink-600/0 group-hover:from-violet-600/10 group-hover:to-pink-600/10 rounded-3xl transition-all duration-500" />
                
                <div className="relative">
                  <div className="mb-6 inline-block p-4 rounded-2xl bg-gradient-to-br from-violet-500/20 to-pink-500/20">
                    <stack.icon size={32} className="text-violet-400" />
                  </div>
                  
                  <h3 className="text-2xl font-bold mb-4 text-violet-300">{stack.name}</h3>
                  
                  <div className="flex flex-wrap gap-2">
                    {stack.items.map((item, j) => (
                      <span
                        key={j}
                        className="px-3 py-1.5 text-sm rounded-full bg-white/5 border border-white/10 text-gray-300 hover:bg-violet-500/20 hover:border-violet-500/50 hover:text-white transition-all duration-300"
                      >
                        {item}
                      </span>
                    ))}
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Projects Section */}
      <div className="relative z-10 py-32 px-4">
        <div className="max-w-7xl mx-auto">
          <h2 className="text-6xl font-black text-center mb-20">
            <span className="bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">
              FEATURED WORKS
            </span>
          </h2>

          <div className="grid md:grid-cols-3 gap-8">
            {projects.map((project, i) => (
              <div
                key={i}
                className="group relative bg-black rounded-3xl overflow-hidden border border-white/10 hover:border-violet-500/50 transition-all duration-500 hover:scale-105"
              >
                <div className={`absolute inset-0 bg-gradient-to-br ${project.gradient} opacity-0 group-hover:opacity-20 transition-opacity duration-500`} />
                
                <div className="relative p-8">
                  <div className="mb-4">
                    <Sparkles className="text-violet-400 mb-4" size={32} />
                    <h3 className="text-3xl font-bold mb-2">{project.title}</h3>
                  </div>
                  
                  <p className="text-gray-400 mb-4 text-lg">{project.desc}</p>
                  
                  <p className="text-sm text-violet-300 font-mono mb-6">{project.tech}</p>
                  
                  <button className="w-full py-3 px-6 rounded-xl bg-gradient-to-r from-violet-600 to-pink-600 font-semibold hover:shadow-2xl hover:shadow-violet-500/50 transition-all duration-300 hover:scale-105">
                    View Project
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Stats Section */}
      <div className="relative z-10 py-32 px-4">
        <div className="max-w-6xl mx-auto">
          <div className="grid md:grid-cols-3 gap-8">
            {[
              { label: 'Projects', value: '50+', icon: Code },
              { label: 'Technologies', value: '30+', icon: Cpu },
              { label: 'GitHub Stars', value: '100+', icon: Star }
            ].map((stat, i) => (
              <div
                key={i}
                className="relative bg-gradient-to-br from-white/5 to-white/0 backdrop-blur-xl rounded-3xl p-12 border border-white/10 text-center group hover:border-violet-500/50 transition-all duration-500"
              >
                <stat.icon className="mx-auto mb-4 text-violet-400 group-hover:scale-110 transition-transform duration-300" size={48} />
                <div className="text-6xl font-black mb-2 bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">
                  {stat.value}
                </div>
                <div className="text-xl text-gray-400">{stat.label}</div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* CTA Section */}
      <div className="relative z-10 py-32 px-4">
        <div className="max-w-4xl mx-auto text-center">
          <h2 className="text-5xl md:text-7xl font-black mb-8">
            <span className="bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">
              Let's Build Something Epic
            </span>
          </h2>
          <p className="text-2xl text-gray-400 mb-12">
            Open to collaborations on AI, Full-Stack, and innovative projects
          </p>
          <a
            href="mailto:itsaman00786@gmail.com"
            className="inline-block py-4 px-12 text-xl font-bold rounded-full bg-gradient-to-r from-violet-600 to-pink-600 hover:shadow-2xl hover:shadow-violet-500/50 transition-all duration-300 hover:scale-110"
          >
            Get In Touch
          </a>
        </div>
      </div>

      <style jsx>{`
        @keyframes float {
          0%, 100% { transform: translateY(0px); }
          50% { transform: translateY(-20px); }
        }
      `}</style>
    </div>
  );
};

export default CinematicGitHubProfile;
