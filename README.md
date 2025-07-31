import 'package:flutter/material.dart';

/// A customizable secondary button widget following the application's theme.
/// This widget provides a reusable button component with a distinct outlined
/// style. It automatically adapts to the current theme's primary color
/// for its border and text, ensuring a consistent look and feel throughout the application.
/// The button takes a [title] string for its text label and an [onTap] callback
/// function to define its behavior when pressed.
class SecondaryButton extends StatelessWidget {
  /// The text displayed on the button.
  final String title;

  /// The callback function that is executed when the button is pressed.
  final VoidCallback onTap;

  /// Creates a primary button widget.
  const SecondaryButton({super.key, required this.title, required this.onTap});

  @override
  Widget build(BuildContext context) {
    final TextStyle? buttonTextStyle = Theme.of(context).textTheme.labelLarge;

    return OutlinedButton(
      onPressed: onTap,
      style: OutlinedButton.styleFrom(
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8.0)),
        side: BorderSide(color: Theme.of(context).colorScheme.primary),
      ),
      child: Text(
        title,
        style: buttonTextStyle?.copyWith(
          color: Theme.of(context).colorScheme.primary,
          fontWeight: FontWeight.bold,
        ),
      ),
    );
  }
}
