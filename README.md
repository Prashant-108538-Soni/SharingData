import 'package:flutter/material.dart';

/// A customizable primary button widget following the application's theme.
/// This widget provides a reusable button component with a distinct primary
/// style. It automatically adapts to the current theme's primary color
/// and text color, ensuring a consistent look and feel throughout the application.
/// The button takes a [title] string for its text label and an [onTap] callback
/// function to define its behavior when pressed.
/// An optional [icon] widget can be provided to display an icon before the title.
class PrimaryButton extends StatelessWidget {
  /// The text displayed on the button.
  final String title;

  /// The callback function that is executed when the button is pressed.
  final VoidCallback onTap;

  /// An optional icon widget to display before the title.
  final Widget? icon;

  /// Creates a primary button widget.
  const PrimaryButton({
    super.key,
    required this.title,
    required this.onTap,
    this.icon,
  });

  @override
  Widget build(BuildContext context) {
    final TextStyle? buttonTextStyle = Theme.of(context).textTheme.labelLarge;

    return ElevatedButton(
      onPressed: onTap,
      style: ElevatedButton.styleFrom(
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Theme.of(context).colorScheme.onPrimary,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8.0)),
      ),
      child:
          icon ==
              null // Conditionally render based on icon presence
          ? Text(
              title,
              style: buttonTextStyle?.copyWith(
                color: Theme.of(context).colorScheme.onPrimary,
                fontWeight: FontWeight.bold,
              ),
            )
          : Row(
              mainAxisSize:
                  MainAxisSize.min, // To keep the row as small as possible
              children: [
                icon!,
                const SizedBox(width: 8.0), // Spacing between icon and text
                Text(
                  title,
                  style: buttonTextStyle?.copyWith(
                    color: Theme.of(context).colorScheme.onPrimary,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ],
            ),
    );
  }
}
