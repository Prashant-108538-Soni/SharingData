import 'package:flutter/material.dart';

/// A pill-shaped label to display event-related status or date information.
///
/// Commonly used for showing short time-related tags like
/// "SCHEDULED", "12 JAN", or "PAID TODAY" inside cards.
class EventExecutionPill extends StatelessWidget {
  /// Text displayed inside the pill (e.g., "17 Sept", "SCHEDULED").
  final String text;

  const EventExecutionPill({
    super.key,
    required this.text,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 4),
      decoration: BoxDecoration(
        color: Colors.orange.shade50,
        border: Border.all(color: Colors.orange),
        borderRadius: BorderRadius.circular(20),
      ),
      child: Text(
        text,
        style: const TextStyle(
          fontSize: 10,
          fontWeight: FontWeight.w500,
          color: Colors.orange,
        ),
      ),
    );
  }
}