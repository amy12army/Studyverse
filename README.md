# Studyverse
Study app for students 
import 'dart:async';
import 'package:flutter/material.dart';

void main() {
  runApp(const StudyverseApp());
}

// ---------------------------------------------------------------------------
// DATA MODELS
// ---------------------------------------------------------------------------

class KPopGroup {
  final String id;
  final String name;
  final Color primaryColor;
  final Color accentColor;
  final String quote;
  final String wallpaperUrl;
  final List<String> avatars;

  KPopGroup({
    required this.id,
    required this.name,
    required this.primaryColor,
    required this.accentColor,
    required this.quote,
    required this.wallpaperUrl,
    required this.avatars,
  });
}

final List<KPopGroup> kpopGroups = [
  KPopGroup(
    id: 'bts',
    name: 'BTS',
    primaryColor: const Color(0xFF2D1B4E),
    accentColor: const Color(0xFF9B51E0),
    quote: "Love yourself, stay focused, and sparkle bright in the Studyverse! ✨",
    wallpaperUrl: 'https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=1000',
    avatars: ['✨', '🌟', '💜', '👑'],
  ),
  KPopGroup(
    id: 'blackpink',
    name: 'BLACKPINK',
    primaryColor: const Color(0xFF1A1A1A),
    accentColor: const Color(0xFFFF69B4),
    quote: "Blackpink in your area! Time to crush this study session and shine. ✨",
    wallpaperUrl: 'https://images.unsplash.com/photo-1509198397868-475647b2a1e5?q=80&w=1000',
    avatars: ['✨', '🌟', '🖤', '💗'],
  ),
  KPopGroup(
    id: 'straykids',
    name: 'Stray Kids',
    primaryColor: const Color(0xFF121212),
    accentColor: const Color(0xFFE50914),
    quote: "Stray Kids everywhere all around the world. Keep your spark alive! ✨",
    wallpaperUrl: 'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?q=80&w=1000',
    avatars: ['✨', '⚡', '🔥', '🎸'],
  ),
  KPopGroup(
    id: 'hybe',
    name: 'HYBE Labels',
    primaryColor: const Color(0xFF0F2027),
    accentColor: const Color(0xFF00D2FF),
    quote: "We believe in music and your limitlessness in the Studyverse! ✨",
    wallpaperUrl: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?q=80&w=1000',
    avatars: ['✨', '🎵', '🎧', '🚀'],
  ),
];

class UserProfile {
  String name;
  String avatarEmoji;
  String gradeClass;
  String mainGoal;
  double dailyFocusGoalHours;
  String bio;
  KPopGroup selectedGroup;
  String customWallpaperUrl;

  UserProfile({
    required this.name,
    required this.avatarEmoji,
    required this.gradeClass,
    required this.mainGoal,
    required this.dailyFocusGoalHours,
    required this.bio,
    required this.selectedGroup,
    required this.customWallpaperUrl,
  });
}

class TodoItem {
  String title;
  String timeSlot;
  bool isCompleted;
  TodoItem({required this.title, required this.timeSlot, this.isCompleted = false});
}

class HabitItem {
  String name;
  int streak;
  bool completedToday;
  HabitItem({required this.name, this.streak = 0, this.completedToday = false});
}

// ---------------------------------------------------------------------------
// MAIN APP ENTRY & STATE MANAGEMENT
// ---------------------------------------------------------------------------

class StudyverseApp extends StatefulWidget {
  const StudyverseApp({Key? key}) : super(key: key);

  @override
  State<StudyverseApp> createState() => _StudyverseAppState();
}

class _StudyverseAppState extends State<StudyverseApp> {
  late UserProfile profile;

  @override
  void initState() {
    super.initState();
    profile = UserProfile(
      name: 'Scholar Star',
      avatarEmoji: '✨',
      gradeClass: 'Grade 11 - Science Track',
      mainGoal: 'Pass Final Exams with Top Rank',
      dailyFocusGoalHours: 4.0,
      bio: 'Exploring the Studyverse with great music and sparkling focus! ✨',
      selectedGroup: kpopGroups[0],
      customWallpaperUrl: kpopGroups[0].wallpaperUrl,
    );
  }

  void updateProfile(UserProfile updated) {
    setState(() {
      profile = updated;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Studyverse',
      debugShowCheckedModeBanner: false,
      theme: ThemeData.dark().copyWith(
        scaffoldBackgroundColor: profile.selectedGroup.primaryColor,
        colorScheme: ColorScheme.dark(
          primary: profile.selectedGroup.accentColor,
          surface: profile.selectedGroup
