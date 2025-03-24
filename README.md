"use client";

import { useState } from "react";
import { Card } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion, AnimatePresence } from "framer-motion";
import { Gift, Heart, Calendar, MapPin, Clock } from "lucide-react";

export default function SurpriseBox() {
  const [opened, setOpened] = useState(false);
  const [showDetails, setShowDetails] = useState(false);

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gradient-to-b from-pink-50 to-pink-100 p-4">
      <AnimatePresence mode="wait">
        {!opened ? (
          <motion.div
            key="gift"
            initial={{ scale: 0.8, rotate: -5 }}
            animate={{ scale: [1, 1.05, 1], rotate: [-5, 5, -5] }}
            transition={{ duration: 2, repeat: Infinity, repeatType: "reverse" }}
            whileHover={{ scale: 1.1 }}
            whileTap={{ scale: 0.95 }}
            exit={{ scale: 1.2, opacity: 0 }}
          >
            <Card
              className="p-8 bg-white shadow-lg rounded-2xl text-center cursor-pointer hover:shadow-2xl transition border-2 border-pink-200"
              onClick={() => setOpened(true)}
            >
              <div className="relative">
                <motion.div animate={{ y: [0, -10, 0] }} transition={{ duration: 1.5, repeat: Infinity }}>
                  <Gift size={64} className="text-pink-500 mx-auto mb-4" />
                </motion.div>
              </div>
              <p className="text-xl font-semibold text-gray-700 mt-2">Clique para abrir seu presente!</p>
              <p className="text-sm text-gray-500 mt-1">Um convite especial aguarda você</p>
            </Card>
          </motion.div>
        ) : (
          <motion.div
            key="surprise"
            initial={{ opacity: 0, y: 20, scale: 0.8 }}
            animate={{ opacity: 1, y: 0, scale: 1 }}
            transition={{ duration: 0.5, type: "spring", stiffness: 300, damping: 15 }}
            className="w-full max-w-md"
          >
            <Card className="p-8 bg-white shadow-lg rounded-2xl text-center overflow-hidden relative">
              <motion.div initial={{ scale: 0 }} animate={{ scale: 1 }} transition={{ delay: 0.3, type: "spring" }}>
                <Heart size={64} className="text-red-500 mx-auto mb-4 drop-shadow-md" />
              </motion.div>
              <motion.div initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ delay: 0.5 }}>
                <h2 className="text-2xl font-bold text-gray-800">Surpresa! 💌</h2>
                <p className="text-gray-600 mt-2">Seu presente é um convite para um momento especial.</p>
              </motion.div>
              <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.7 }} className="mt-6">
                <p className="text-gray-700 font-semibold mt-4">📍 Local: [Defina o lugar]</p>
                <p className="text-gray-700 font-semibold">🗓 Data: [Escolha um dia]</p>
                <p className="text-gray-700 font-semibold">⏰ Horário: [Defina o horário]</p>
                <div className="mt-6 flex gap-4 justify-center">
                  <Button className="bg-red-500 hover:bg-red-600 text-white">Sim, é claro! 🎉</Button>
                  <Button variant="outline" onClick={() => setShowDetails(true)}>
                    Me conta mais 🤔
                  </Button>
                </div>
              </motion.div>
            </Card>
            <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 1 }} className="mt-4 text-center">
              <Button variant="ghost" size="sm" className="text-gray-500 hover:text-gray-700" onClick={() => setOpened(false)}>
                Voltar ao presente
              </Button>
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
}
