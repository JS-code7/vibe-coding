📌 Product Requirements Document (PRD)

BrainyBox → fun + learning in a sandbox.

Project: Mini Machine Learning Playground
Version: v1.0
Owner: Jeet Soni
Last Updated: 30 Aug 2025

1. Overview

The Mini Machine Learning Playground is an interactive, web-based educational app that allows users to explore core machine learning concepts without writing code. It integrates a beautiful Lovable-built frontend with a Supabase backend for persistence, sharing, and gamification. Users can experiment with datasets, tune model parameters, visualize results, and track progress.

2. Objectives

Make ML approachable and visual for students, teachers, and beginners.

Allow parameter tweaking + real-time visualization (via TensorFlow.js).

Enable users to save, share, and replay experiments.

Provide gamified learning with badges and challenges.

Support both individual learners and teachers in classrooms.

3. Target Users

Students / Beginners: Learn ML concepts interactively.

Educators: Demonstrate concepts in live classes.

Hobbyists / Self-learners: Play with ML without complex setup.

4. User Stories

As a student, I can change ML parameters (learning rate, clusters, etc.) and see visual updates instantly.

As a teacher, I can save and share experiments with my students.

As a user, I can view leaderboards/challenges and earn badges (e.g., “90% Accuracy”).

As a guest, I can explore public experiments without logging in.

As a registered user, I can save experiments, replay runs, and track my achievements.

5. Core Features
a. Home / Dashboard

Hero section with tagline: “Play with Machine Learning – No Code, Just Fun!”

Cards linking to playgrounds: Classification, Regression, Clustering.

Dark/Light mode toggle.

b. Playgrounds (per ML type)

Dataset Selection (Iris, Housing, Spiral, Gaussian blobs).

Model Selection (Logistic Regression, Decision Tree, kNN, Linear, Polynomial, K-Means, DBSCAN).

Parameter Controls (sliders, dropdowns).

Run Button → Triggers TF.js computation + stores run in Supabase.

Visualization Panel (decision boundaries, regression lines, cluster coloring).

Metrics Panel (Accuracy, Loss, R², etc.).

Explanation Panel (plain-English explanations).

c. Experiments

Save experiment configuration (dataset, model, params).

Share experiment (via Supabase share_token + Edge Function).

Public experiments gallery (list of shared setups).

d. Gamification

Badges for hitting thresholds (accuracy ≥90%, low error, etc.).

Leaderboard (optional future expansion).

e. Storage

Datasets bucket: Public datasets & synthetic examples.

Exports bucket: Private user visualizations (e.g., saved charts).

6. Architecture
Frontend (Lovable + TF.js)

Framework: React + TailwindCSS + Framer Motion

Charts/Plots: Recharts or Plotly.js

ML Engine: TensorFlow.js (in-browser)

Realtime Updates: Supabase Realtime for runs

Backend (Supabase)

Auth: Supabase Auth (Email, OAuth)

Database:

profiles: user info

datasets: dataset catalog

models: ML model catalog

experiments: saved configurations

runs: execution results

achievements: gamified badges

Storage Buckets: datasets (public), exports (private)

Edge Functions:

create-share-link → Generate shareable link

public-experiments → List/search shared experiments

record-run → Securely record run results

RLS Policies: Owner-only access, public read for shared data.

7. APIs & Data Flows

Create Experiment (RPC)

Input: title, dataset_id, model_id, parameters

Output: experiment record

Run Model (Frontend → TF.js → record_run RPC)

TF.js computes metrics/artifacts → stored in Supabase runs

Share Experiment (Edge Function)

Generates share_token → experiment becomes public

Realtime Subscriptions

Frontend subscribes to runs → auto-update metrics dashboard

Public Experiments (Edge Function)

Paginated list with search

8. Design / UI-UX

Look & Feel: Playful but professional, pastel gradients, card-based layout.

Playground Layout:

Left: Controls (dataset, model, sliders).

Right: Visualization + Metrics + Explanation.

Onboarding: Step-by-step tooltips.

Animations: Smooth transitions with Framer Motion.

Accessibility: Keyboard navigation + color-blind friendly plots.

9. Success Metrics

Avg. session > 5 minutes.

≥50% of users run at least 2 experiments per visit.

≥20% of registered users share experiments.

Badge/achievement system engagement (≥10% of users unlock at least one badge).

10. Future Enhancements

Upload custom CSV datasets.

Add Neural Network Playground (2-layer perceptron).

Add Reinforcement Learning Playground (CartPole demo).

Classroom mode (multi-tenant orgs for teachers/students).

Export experiment results to PDF/PNG.

11. Risks & Mitigation

Performance bottlenecks in TF.js → Use smaller datasets / downsampled visualizations.

Abuse of storage → Apply quotas + file size limits.

Security → Strict RLS + only use service-role key in Edge Functions.

12. Timeline (MVP)

Week 1–2: Backend setup (Supabase schema, RPCs, policies, seed data).

Week 3–4: Lovable frontend pages (Home, Playgrounds, Visualization).

Week 5: TF.js integration + Supabase Realtime for runs.

Week 6: Shareable experiments + badges.

Week 7: QA, bug fixing, UI polish.

Week 8: Beta launch.
