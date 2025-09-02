import { useState } from "react..";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Compass, GraduationCap, User } from "lucide-react";
import { motion, AnimatePresence } from "framer-motion";

export default function CareerAdvisorApp() {
  const [page, setPage] = useState("dashboard");

  const pages = {
    dashboard: <Dashboard />,
    explore: <Explore />,
    assessments: <Assessments />,
    profile: <Profile />,
  };

  return (
    <div className="min-h-screen flex flex-col bg-gradient-to-br from-blue-50 via-white to-purple-50">
      {/* Header */}
      <motion.header
        initial={{ y: -80, opacity: 0 }}
        animate={{ y: 0, opacity: 1 }}
        transition={{ duration: 0.6 }}
        className="bg-white/80 backdrop-blur-md shadow p-4 flex justify-between items-center sticky top-0 z-50"
      >
        <motion.h1
          initial={{ scale: 0.8, opacity: 0 }}
          animate={{ scale: 1, opacity: 1 }}
          transition={{ duration: 0.5 }}
          className="text-2xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600"
        >
          EduCareer Advisor
        </motion.h1>
        <nav className="flex gap-4">
          {Object.keys(pages).map((key) => (
            <motion.div whileHover={{ scale: 1.1 }} whileTap={{ scale: 0.95 }} key={key}>
              <Button
                variant={page === key ? "default" : "ghost"}
                onClick={() => setPage(key)}
              >
                {key.charAt(0).toUpperCase() + key.slice(1)}
              </Button>
            </motion.div>
          ))}
        </nav>
      </motion.header>

      {/* Main Content with Animation */}
      <main className="flex-1 p-6">
        <AnimatePresence mode="wait">
          <motion.div
            key={page}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, y: -20 }}
            transition={{ duration: 0.5 }}
          >
            {pages[page]}
          </motion.div>
        </AnimatePresence>
      </main>
    </div>
  );
}

function Dashboard() {
  return (
    <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
      {["Career Recommendations", "Education Paths", "Progress Tracker"].map((title, idx) => (
        <motion.div
          key={title}
          initial={{ opacity: 0, scale: 0.9 }}
          animate={{ opacity: 1, scale: 1 }}
          transition={{ delay: idx * 0.2, duration: 0.6 }}
        >
          <Card className="shadow-lg hover:shadow-2xl hover:-translate-y-1 transition rounded-2xl overflow-hidden bg-white/90 backdrop-blur">
            <CardContent className="p-6">
              <h2 className="text-xl font-semibold mb-2 text-blue-700">{title}</h2>
              <p className="text-gray-600">
                {title === "Career Recommendations" && "Explore jobs tailored to your skills and interests."}
                {title === "Education Paths" && "Find courses and degrees that align with your goals."}
                {title === "Progress Tracker" && "Track your journey and milestones toward success."}
              </p>
            </CardContent>
          </Card>
        </motion.div>
      ))}
    </div>
  );
}

function Explore() {
  return (
    <div>
      <motion.h2
        initial={{ x: -30, opacity: 0 }}
        animate={{ x: 0, opacity: 1 }}
        transition={{ duration: 0.6 }}
        className="text-2xl font-bold mb-4 flex items-center gap-2 text-purple-700"
      >
        <Compass /> Explore Careers & Courses
      </motion.h2>
      <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        {"Data Scientist, Software Engineer, Digital Marketer, UX Designer, Project Manager, AI Specialist".split(", ").map((career, idx) => (
          <motion.div
            key={career}
            initial={{ opacity: 0, y: 30 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: idx * 0.1, duration: 0.5 }}
            whileHover={{ scale: 1.05, rotate: 1 }}
            whileTap={{ scale: 0.95 }}
          >
            <Card className="shadow-md hover:shadow-xl transition transform rounded-2xl bg-white/90 backdrop-blur">
              <CardContent className="p-4">
                <h3 className="font-semibold text-lg text-blue-800">{career}</h3>
                <p className="text-gray-600 text-sm">Learn more about the path, skills, and education needed.</p>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>
    </div>
  );
}

function Assessments() {
  return (
    <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ duration: 0.6 }}>
      <h2 className="text-2xl font-bold mb-4 flex items-center gap-2 text-blue-700"><GraduationCap /> Career Assessments</h2>
      <p className="text-gray-600 mb-6">Take quizzes to discover careers that match your personality and skills.</p>
      <motion.div whileHover={{ scale: 1.05 }} whileTap={{ scale: 0.95 }}>
        <Button className="bg-gradient-to-r from-blue-600 to-purple-600 text-white shadow-lg">Start Assessment</Button>
      </motion.div>
    </motion.div>
  );
}

function Profile() {
  return (
    <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ duration: 0.6 }}>
      <h2 className="text-2xl font-bold mb-4 flex items-center gap-2 text-purple-700"><User /> Your Profile</h2>
      <motion.div
        initial={{ scale: 0.9, opacity: 0 }}
        animate={{ scale: 1, opacity: 1 }}
        transition={{ duration: 0.6 }}
      >
        <Card className="shadow-md max-w-md rounded-2xl bg-white/90 backdrop-blur">
          <CardContent className="p-6">
            <h3 className="font-semibold text-lg text-blue-800">John Doe</h3>
            <p className="text-gray-600">Aspiring Data Scientist</p>
            <p className="text-gray-600 mt-2 text-sm">Saved Careers: Data Scientist, AI Specialist</p>
          </CardContent>
        </Card>
      </motion.div>
    </motion.div>
  );
}

