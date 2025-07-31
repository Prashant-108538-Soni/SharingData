import 'package:flutter/material.dart';

/// A StatelessWidget that displays an event's date and a descriptive string
/// in a pill-shaped container. It's designed to visually highlight important
/// time-related information in a concise format.
class EventExecutionPill extends StatelessWidget {
  /// Creates an [EventExecutionPill] widget.
  ///
  /// The [eventDate] and [eventString] are required to display the event information.
  const EventExecutionPill({super.key, required this.text});

  /// The date of the event to be displayed (e.g., "12th Jan 2025").
  final String text;

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 4),
      decoration: BoxDecoration(
        border: Border.all(color: Colors.orange),
        borderRadius: BorderRadius.circular(20),
        color: Colors.orange.shade50,
      ),
      child: Text(
        text,
        style: const TextStyle(color: Colors.orange, fontWeight: FontWeight.w500, fontSize: 10),
      ),
    );
  }
}
